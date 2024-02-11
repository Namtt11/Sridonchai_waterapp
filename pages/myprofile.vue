<template>
  <div @click="Back"><Icon name="mdi:arrow-back-circle" size="36"/></div>
    <div class="flex h-dvh">
      <div class="my-auto w-full mx-3 border rounded-md p-3 ">
        <div class="text-2xl text-center font-bold">
          ข้อมูลส่วนตัว
        </div>
        <div>
            WHO AM I : {{ whoami }}
        </div>
  
        <label class="form-control w-full">
        <div class="label">
          <span class="label-text">E-mail</span>
        </div>
        <input v-model="loginForm.username" type="text" placeholder="E-mail" class="input input-bordered w-full" />
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
      </label>
  
  
        
        <button @click="login" className="btn btn-block mt-3 bg-green-500 text-white text-xl font-bold">บันทึก</button>
        <button @click="login" className="btn btn-block mt-3 bg-red-500 text-white text-xl font-bold">ออกจากระบบ</button>
      </div>
  
      <dialog ref="alertModal" id="my_modal_3" class="modal">
        <div class="modal-box">
  
          <h3 class="font-bold text-lg">Alert</h3>
          <p class="py-4">{{hasErrors.message}}</p>
        </div>
        <form method="dialog" class="modal-backdrop">
          <button>close</button>
        </form>
      </dialog>
  
    </div>
  </template>
  
  <script lang="ts" setup>
  
  let loginForm = reactive({
    username: "",
    password: "",
  })
  
  let hasErrors = reactive({
    username: null as any,
    password: null,
    message : ""
  })
  
  const alertModal = ref<HTMLDialogElement>()
  
  const router = useRouter()
  const headers = useRequestHeaders(['cookie'])
  
  async function  login() {
    console.log(loginForm)
    console.log(loginForm.username, loginForm.password)
  
    let loginSuccess = false;
    let result = await useFetch("http://localhost:8000/api/method/logout",{
      method : "post",
      credentials : "include",
    
    })
  
    console.log(result)
    loginSuccess = result.status.value === "success"
  
  
    if (loginSuccess) {
      router.push({ path: '/logout' })
    } else {
      alertModal.value?.showModal()
      
  
  
      hasErrors.message = result.error.value?.data?.message
    }
  }
  let whoamiresult = await useFetch("http://localhost:8000/api/method/frappe.auth.get_logged_user",{
  credentials : "include"
})
let whoami = whoamiresult.data
async function  Back() {
  router.push({ path: '/home' })
}
  </script>
  
  <style></style>