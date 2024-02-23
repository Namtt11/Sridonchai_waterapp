<template>
    <div class="flex h-dvh">
      <div class="w-full">
  
        <div class="my-6 text-2xl text-center rounded-md border-sky-500">เพิ่มการใช้น้ำเดือน</div>
  
        <div class="text-center">ข้อมูลการใช้น้ำย้อนหลัง <Icon name="ion:water-outline" /></div>
  
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
            <tr v-for ="(row, index) in userInfo" :key="index">
            <td>{{ row.month }}</td>
            <td>{{ row.total_unit }}</td>
            <td>{{ row.total_price }}</td>
          </tr>
          </tbody>
        </table>
      </div>
  
        <div class="mt-3 text-center text-xl">กรอกข้อมูลปัจจุบัน</div>
  
        <!-- Current Meter -->
        <div class="mt-3 flex space-x-10 justify-center">
          <div class="mx-3 justify-start">เลขมิเตอร์ปัจจุบัน</div>
          <div><input v-model="currentMeter" type="text" placeholder="0" class="input input-bordered input-primary w-24 max-w-xs" /></div>
          <div class="mr-3">หน่วย</div>
        </div>
  
        <!-- Price -->
        <div class="mt-4 flex space-x-10 justify-center">
          <div class="mx-3 justify-start">ราคา</div>
          <div><input v-model="price" type="text" placeholder="0" class="input input-bordered input-primary w-24 max-w-xs" /></div>
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
        <p class="py-4">ค่าบำรุงมิเตอร์ : {{ config.message.meter_maintenance_cost }} บาท</p>
        <p class="py-4">สรุปยอดทั้งหมดเป็นราคา :{{ all }} บาท</p>


        <div class="mt-3 flex space-x-10 justify-center">
          <div > 
            <form method="dialog" class="modal-backdrop">
            <button class="btn btn-error  bg-red-500" @click="">ยกเลิก</button>
            </form>
          </div>
          <div><button class="btn  bg-green-500" @click="record">บันทึก</button></div>
        </div>
      </div>
    </dialog>

    </div>


  </template>
  
  <script lang="ts" setup>
  import { ref } from 'vue';

  const route = useRoute()
  console.log(route.params)
  const name = route.params.name
  

let  Userdata  = await $fetch<{
name: string ; message: {} 
}>("http://localhost:8000/api/method/sridonchai.sridonchai.api.get_info_house",{
  method: "post",
  headers : {
    "Content-Type" : 'application/json'
  },
  body:{
    "name": name
  },
  credentials : "include",

  })



  
let config  = await $fetch<{
name: string ; message: {} 
}>("http://localhost:8000/api/method/sridonchai.sridonchai.api.get_config",{
  method: "post",
  headers : {
    "Content-Type" : 'application/json'
  },
  // body:{
  //   "unit_per_month": bath
  // },
  credentials : "include",

  })

const userInfo = ref(Userdata.message.Usages)


  
  const month = ref({
    month: new Date().getMonth(),
    year: new Date().getFullYear()
  });
  
  

  const router = useRouter()
  async function  Cancel(id:string) {
  router.push({ path: '/info/'+id })
}
const alertModal = ref<HTMLDialogElement>()

// async function record() {
//   alertModal.value?.showModal()
// }


const currentMeter = ref()
const water_price = ref(config.message.unit_per_month)
const maintenance_cost = ref(config.message.meter_maintenance_cost)
const last_meter = ref('100')
const price = ref()
const water_usage = currentMeter.value - last_meter.value 
const sum_price = computed(() => water_usage.value * water_price.value);
const all = sum_price.value + maintenance_cost.value;


price.value === sum_price


console.log(sum_price)
async function record() {
  alertModal.value?.showModal()
  
console.log(all.value)
}
  </script>
  
  