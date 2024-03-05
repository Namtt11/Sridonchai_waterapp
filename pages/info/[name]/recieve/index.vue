<template>
    <div class="flex h-dvh">
      
        <div class="my-auto w-full mx-3 border rounded-md p-3 ">
          <div @click="Back"><Icon name="mdi:arrow-back-circle" size="36"/></div>
            <div class="text-2xl text-center font-bold">
            รับชำระเงิน
            </div>
      <div class="overflow-y-auto mt-3 h-full" 
          v-bind:key="data.name"
          v-for="data in Userdata.message ">
      <div class="grid gap-2">
        <div
        @click="GoInfo(data.name)"
          class="flex-col border-solid border-2 border-gray-300 p-3 bg-red-300">
          <div class="text-md font-bold"  >ค่าน้ำปะปารอบเดือน {{ data.month }}</div>
          <div class="text-md font-bold"  >ยอดค้างชำระ {{ data.total_price }} บาท</div>
          <span class="align-text-bottom">
            <span>สถานะ : ไม่ได้ชำระเงิน</span>
          </span>
        </div>
      </div>
    </div>
        </div>
    </div>
   
           
</template>

<script lang="ts" setup>


const route = useRoute()
const name = route.params.name

let  Userdata  = await $fetch<{
name: string ; message: {} 
}>("http://localhost:8000/api/method/sridonchai.sridonchai.api.get_bill",{
  method: "post",
  headers : {
    "Content-Type" : 'application/json'
  },
  body:{
    "name": name
  },
  credentials : "include",
  

  })
   console.log(Userdata)

const router = useRouter();
async function Back(id: string) {
  router.push({ path: `/info/${route.params.name}`});
}
async function GoInfo(id: string) {
  router.push({ path: `/info/${route.params.name}/recieve/${id}`});
}
</script>