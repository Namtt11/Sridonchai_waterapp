<template>
  <div @click="Back"><Icon name="mdi:arrow-back-circle" size="36"/></div>
    <div class="flex h-dvh">
      <div class="my-auto w-full mx-3 border rounded-md p-3 ">
        <div class="text-2xl text-center font-bold">
          ข้อมูลส่วนตัว
        </div>
        <div>ชื่อผู้ใช้ : {{ user.message.username }}</div>
        <div>E-mail : {{ user.message.email }}</div>
        <div>ชื่อ : {{ user.message.first_name }}</div>
        <div>นามสกุล : {{ user.message.last_name }}</div>
        
        <!-- <label class="form-control w-full"> -->
        <!-- <div class="label">
          <span class="label-text">E-mail {{ user.message.email }}</span>
        </div>
        <input  type="text" placeholder={{ user.message.email }} class="input input-bordered w-full" />
      </label>

      
      <label class="form-control w-full">
        <div class="label">
          <span class="label-text">ชื่อ</span>
        </div>
        <input  type="text" placeholder="ชื่อ" class="input input-bordered w-full" />
      </label>
  
      <label class="form-control w-full">
        <div class="label">
          <span class="label-text">นามสกุล</span>
        </div>
        <input type="text" placeholder="นามสกุล" class="input input-bordered w-full" />
      </label> -->
  
  
        
        <!-- <button @click="login" className="btn btn-block mt-3 bg-green-500 text-white text-xl font-bold">บันทึก</button> -->
        <button @click="logout" className="btn btn-block mt-3 bg-red-500 text-white text-xl font-bold">ออกจากระบบ</button>
      </div>
  
      
  
    </div>
  </template>
  
  <script lang="ts" setup>
  

  const router = useRouter()

  let  currentUser  = await useFetch("http://localhost:8000/api/method/sridonchai.sridonchai.api.get_current_user_info",{
    credentials : "include"
  })
  let user = currentUser.data
  
  let whoamiresult = await useFetch("http://localhost:8000/api/method/frappe.auth.get_logged_user",{
  credentials : "include"
})
let whoami = whoamiresult.data

async function  Back() {
  router.push({ path: '/home' })
}
async function  logout() {
  router.push({ path: '/logout' })
}

  </script>
  
  <style></style>