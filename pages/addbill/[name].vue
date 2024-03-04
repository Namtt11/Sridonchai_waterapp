<template>
  <div class="flex h-dvh">
    <div class="w-full">

      <div class="my-6 text-2xl text-center rounded-md border-sky-500" v-once>เพิ่มการใช้น้ำเดือน
        <p>{{ formattedDate }}</p>
      </div>

      <div class="text-center">ข้อมูลการใช้น้ำย้อนหลัง
        <Icon name="ion:water-outline" />
      </div>

      <div class="overflow-x-auto">
        <table class="table table-zebra">
          <!-- head -->
          <thead>
            <tr>
              <th>เดือน</th>
              <th>จำนวนการใช้น้ำ (หน่วย)</th>
              <th>ยอดชำระ (บาท)</th>
            </tr>
          </thead>
          <tbody>
            <!-- rows -->
            <tr v-for="(row, index) in userInfo" :key="index">
              <td v-if="index < 3">{{ row.month }}</td>
              <td v-if="index < 3">{{ row.total_unit }}</td>
              <td v-if="index < 3">{{ row.total_price }}</td>
              <!-- <td>{{ index }}</td> -->
            </tr>
          </tbody>
        </table>
      </div>

      <div class="mt-3 text-center text-xl">กรอกข้อมูลปัจจุบัน</div>
      <div class="mt-3 text-center">เลขมิเตอร์เดือนก่อน {{ last_meter }} หน่วย</div>
      <!-- Current Meter -->
      <div class="mt-3 flex space-x-10 justify-center">
        <div class="mx-3 justify-start">เลขมิเตอร์ปัจจุบัน</div>
        <div><input v-model="currentMeter" type="text" placeholder="0"
            class="input input-bordered input-primary w-24 max-w-xs" /></div>
        <div class="mr-3">หน่วย</div>
      </div>

      <!-- Price -->
      <div class="mt-4 flex space-x-10 justify-center">
        <div class="mx-3 justify-start">ราคา</div>
        <div><input v-model="price" type="text" placeholder="0"
            class="input input-bordered input-primary w-24 max-w-xs" /></div>
        <div class="mr-3">บาท</div>
      </div>

      <!-- Buttons -->
      <div class="mt-3 flex space-x-10 justify-center">
        <div> <button class="btn  bg-red-500" @click="Cancel(name)">ยกเลิก</button></div>
        <div><button class="btn  bg-green-500" @click="record">บันทึก</button></div>
      </div>
    </div>


    <dialog ref="alertModal" id="my_modal_3" class="modal">
      <div class="modal-box">

        <h3 class="font-bold text-lg text-center ">สรุปยอด</h3>
        <p class="py-4">เลขมิเตอร์ที่จดครั้งล่าสุด :{{ last_meter }} หน่วย</p>
        <p class="py-4">เลขมิเตอร์ที่จดปัจจุบัน : {{ currentMeter }} หน่วย</p>
        <p class="py-4">จำนวนการใช้น้ำ :{{ water_usage }} หน่วย</p>
        <p class="py-4">ราคาค่าน้ำต่อหน่วย : {{ config.message.unit_per_month }} บาท</p>
        <p class="py-4">ค่าน้ำเดือนปัจจุบัน : {{ sum_price }} บาท</p>
        <p class="py-4">สรุปยอดทั้งหมดเป็นราคา :{{ sum_price }} บาท</p>


        <div class="mt-3 flex space-x-10 justify-center">
          <div>
            <form method="dialog" class="modal-backdrop">
              <button class="btn btn-error  bg-red-500" @click="">ยกเลิก</button>
            </form>
          </div>
          <div><button class="btn  bg-green-500" @click="put_data">บันทึก</button></div>
        </div>
      </div>
    </dialog>

  
  </div>
</template>
  
<script lang="ts" setup>


let now = new Date();
const formattedDate = `${now.getFullYear()}-${(now.getMonth() + 1).toString().padStart(2, '0')}`;

let currentMonth = now.getMonth() + 1;
let currentYear = now.getFullYear();

// หากเดือนปัจจุบันเป็นเดือนมกราคม (1) ให้เปลี่ยนเป็นเดือนธันวาคม (12) ของปีที่แล้ว
let lastMonth = currentMonth === 1 ? 12 : currentMonth - 1;

// หากเดือนเป็นเดือนมกราคม ให้ปีลดลงไปอีก 1 ปี
let lastYear = currentMonth === 1 ? currentYear - 1 : currentYear;

// สร้างวัตถุ Date จากเดือนก่อนหน้า
let lastMonthDate = new Date(lastYear, lastMonth - 1);

// กำหนดรูปแบบเดือนก่อนหน้าในรูปแบบ 'YYYY-MM'
const formattedLastMonthDate = `${lastMonthDate.getFullYear()}-${(lastMonthDate.getMonth() + 1).toString().padStart(2, '0')}`;

console.log("เดือนก่อนหน้า:", formattedLastMonthDate);


import { ref } from 'vue';

const route = useRoute()
console.log(route.params)
const name = route.params.name


let Userdata = await $fetch<{
  name: string; message: {}
}>("http://localhost:8000/api/method/sridonchai.sridonchai.api.get_info_house", {
  method: "post",
  headers: {
    "Content-Type": 'application/json'
  },
  body: {
    "name": name
  },
  credentials: "include",

})




let config = await $fetch<{
  name: string; message: {}
}>("http://localhost:8000/api/method/sridonchai.sridonchai.api.get_config", {
  method: "post",
  headers: {
    "Content-Type": 'application/json'
  },

  credentials: "include",

})

let lastmeter = await $fetch<{
  name: string; message: {}
}>("http://localhost:8000/api/method/sridonchai.sridonchai.api.get_lastemeter_unit", {
  method: "post",
  headers: {
    "Content-Type": 'application/json'
  },
  body: {
    "name": name ,
    "month" : formattedLastMonthDate
  },
  credentials: "include",

})





const userInfo = ref(Userdata.message.Usages)


const router = useRouter()
async function Cancel(id: string) {
  router.push({ path: '/info/' + id })
}
const alertModal = ref<HTMLDialogElement>()
const alertModal2 = ref<HTMLDialogElement>()


const currentMeter = ref()
const water_price = ref(parseInt(config.message.unit_per_month))
const last_meter = ref(parseInt(lastmeter.message.current_meter_unit));
const price = ref()
const water_usage = computed(() => {
  const usage = currentMeter.value - last_meter.value;
  return Math.max(0, usage);
});
const sum_price = computed(() => {
  if (water_usage.value * water_price.value === 0) {
    return price.value;
  } else {
    return water_usage.value * water_price.value;
  }
});

// 

console.log(sum_price)
async function record() {
  alertModal.value?.showModal()
}



async function put_data(id : string) {
  router.push({ path: '/recieve/' + id })
  // console.log({

  //   name: "1382530f3a",
  //   owner: "bewphisit@gmail.com",
  //   house: name,
  //   user: "bewphisit@gmail.com",
  //   last_meter_unit: last_meter.value,
  //   current_meter_unit: currentMeter,
  //   total_unit: water_usage.value,
  //   total_price: sum_price.value
  // })
  let result = await $fetch("http://localhost:8000/api/resource/Water Usage", {
    method: "post",

    headers: {
      "Accept": "application/json",
      "Content-Type": 'application/json'
    },
    body: {
      owner: "bewphisit@gmail.com",
      house: name,
      user: "bewphisit@gmail.com",
      month: formattedDate ,
      last_meter_unit: last_meter.value,
      current_meter_unit: currentMeter.value,
      total_unit: water_usage.value,
      total_price: sum_price.value
    },
    credentials: "include",


  })
  console.log(result)
}


</script>
  
  