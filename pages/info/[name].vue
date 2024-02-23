<template>
    <div>
      <div class="flex flex-col mx-3 h-dvh relative">
        <div class="flex flex-col sticky top-0 pt-3 bg-white">
          <div @click="Back"><Icon name="mdi:arrow-back-circle" size="36"/></div>
            <div class="text-2xl text-center font-bold">
              ข้อมูลผู้ใช้น้ำ
            <Icon name="mdi:account" />
            </div>
      
          <div class="m-3">
            <div class="m-3 p-2 border rounded-md border-sky-500">
              <p><b>ชื่อผู้ใช้น้ำ</b>  : {{ Userdata.message.owner_name }}</p>
              <p><b>ที่อยู่</b>  :  {{ Userdata.message.house_number }}</p>
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
            <tr v-for="(row, index) in userInfo" :key="index">
            <td>{{ row.month }}</td>
            <td>{{ row.total_unit }}</td>
            <td>{{ row.total_price }}</td>
          </tr>
          </tbody>
        </table>
        </div>
      <div class="sticky top-100">
        <button class="btn btn-block mt-3 bg-red-500 text-white text-xl font-bold" @click="record">
        รับชำระเงิน
        <icon name="icon-park-outline:bill" />
      </button>
      <button class="btn btn-block mt-3 bg-sky-500 text-white text-xl font-bold" @click="NextPageAddbill(name)">
        เพิ่มบิลการใช้น้ำ
        <icon name="icon-park-outline:bill" />
      </button>
      <dialog ref="alertModal" id="my_modal_3" class="modal">
      <div class="modal-box">

        <h3 class="font-bold text-lg text-center ">แจ้งสรุปยอดชำระ</h3>
        <p class="py-4">ยอดค้างชำระทั้งหมด :{{ overdue }} บาท</p>


        <div class="mt-3 flex space-x-10 justify-center">
          <div > 
            <form method="dialog" class="modal-backdrop">
            <button class="btn btn-block bg-red-500" @click="">ยกเลิก</button>
            </form>
          </div>
          <div><button class="btn bg-green-500" @click="record">รับเงินแล้ว</button></div>
        </div>
      </div>
    </dialog>
      </div>
      </div>
      </div>
    </div>

  </template>
  
  <script lang="ts" setup>
  
  const route = useRoute()
  console.log(route.params)
  
  const name = route.params.name
  
  import { useRouter } from 'vue-router';
import { useFetch } from '@vueuse/core';



// const { data: userInfo } = useFetch('http://localhost:8000/api/method/sridonchai.sridonchai.api.get_info_house');
// console.log(userInfo);

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

const router = useRouter();
async function  NextPageAddbill(id:string) {
router.push({ path: '/addbill/'+id })
}
async function  Back() {
router.push({ path: '/homeselect' })
}


let  OverdueData  = await $fetch<{
name: string ; message: {} 
}>("http://localhost:8000/api/method/sridonchai.sridonchai.api.get_overdue_house",{
  method: "post",
  headers : {
    "Content-Type" : 'application/json'
  },
  body:{
    "name": name
  },
  credentials : "include",
  

  })

  const overdue = ref<string>(OverdueData.message.overdue)

const alertModal = ref<HTMLDialogElement>()
async function record() {
  alertModal.value?.showModal()
  console.log(OverdueData)
}
 
  
  </script>
