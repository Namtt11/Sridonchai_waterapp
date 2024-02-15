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
            <tr v-for="(row, index) in userInfo" :key="index">
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
          <div> <button class="btn btn-error" @click="Cancel(name)">ยกเลิก</button></div>
          <div><button class="btn btn-success">บันทึก</button></div>
        </div>
  
      </div>
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
  
  console.log(Userdata.message)
const userInfo = ref(Userdata.message.Usages)


  
  const month = ref({
    month: new Date().getMonth(),
    year: new Date().getFullYear()
  });
  
  const currentMeter = ref('');
  const price = ref('');

  const router = useRouter()
  async function  Cancel(id:string) {
  router.push({ path: '/info/'+id })
}
  
  </script>
  
  <style>
  
  </style>