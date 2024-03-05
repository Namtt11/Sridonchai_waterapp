<template>
    <div class="flex h-dvh">
        <div class="my-auto w-full mx-3 border rounded-md p-3 ">
            <div class="text-2xl text-center font-bold">
           
            ยืนยันชำระเงิน
            </div>
            
      <button @click="getmoney(name)" className="btn btn-block mt-3 bg-green-500 text-white text-xl font-bold">ได้รับเงินแล้ว</button>
      <button @click="No" className="btn btn-block mt-3 bg-red-500 text-white text-xl font-bold">ยังไม่ได้รับเงิน</button>
        </div>
    </div>
   
           
</template>

<script setup lang="ts">

const router = useRouter();
const route = useRoute()
console.log(route.params)
const name = route.params.usage

let now = new Date();
const formattedDate = `${now.getFullYear()}-${(now.getMonth() + 1).toString().padStart(2, '0')}-${now.getDate().toString().padStart(2, '0')}`;

async function getmoney() { 

const res = await $fetch<{name: string , message: {} }>('http://localhost:8000/api/resource/Water Usage/'+ name , {
    method: "put",

    headers: {
      "Accept": "application/json",
      "Content-Type": 'application/json'
    },
    body: {
     
        date_recieve : formattedDate ,
    },
    credentials: "include",

    
  })
  router.push({ path: `/info/${route.params.name}/recieve`})
};

async function No() {
  router.push({ path: `/info/${route.params.name}/recieve`}) 
}

  





</script>