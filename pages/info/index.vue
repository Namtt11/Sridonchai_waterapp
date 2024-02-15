<template>
  <div class="flex flex-col mx-3 h-dvh relative">
    <div class="flex flex-col sticky top-0 pt-3 bg-white">
      <div @click="Back"><Icon name="mdi:arrow-back-circle" size="36"/></div>
      <div class="text-2xl text-center font-bold">
        ข้อมูลผู้ใช้น้ำ
        <Icon name="mdi:account" />
      </div>
      
      <div class="m-3">
        <div class="m-3 p-2 border rounded-md border-sky-500">
          <p><b>ชื่อผู้ใช้น้ำ</b>{{ userInfo?.owner_name }}</p>
          <p><b>ที่อยู่</b>{{ userInfo?.house_number }}</p>
        </div>
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
            <tr v-for="(row, index) in userInfo?.usages" :key="index">
            <td>{{ row.month }}</td>
            <td>{{ row.totalUnit }}</td>
            <td>{{ row.totalPrice }}</td>
          </tr>
          </tbody>
        </table>
      </div>

      <button class="btn btn-block mt-3 bg-sky-500 text-white text-xl font-bold" @click="NextPageAddbill">
        เพิ่มบิลการใช้น้ำ
        <icon name="icon-park-outline:bill" />
      </button>

    </div>
  </div>
</template>

<script setup lang="ts">
import { useRouter } from 'vue-router';
import { useFetch } from '@vueuse/core';



// const { data: userInfo } = useFetch('http://localhost:8000/api/method/sridonchai.sridonchai.api.get_info_house');
// console.log(userInfo);

let  Userdata  = await $fetch<{ message: {} }>("http://localhost:8000/api/method/sridonchai.sridonchai.api.get_info_house",{
  method: "post",
  headers : {
    "Content-Type" : 'application/json'
  },
  credentials : "include",
  

  })
  
  
console.log(Userdata)
const userInfo = ref(Userdata.name)



const router = useRouter();
async function  NextPageAddbill() {
router.push({ path: '/Addbill' })
}
async function  Back() {
router.push({ path: '/homeselect' })
}
 
</script>
