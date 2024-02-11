<template>
  <div class="flex h-dvh">
    <div class="my-auto w-full mx-3 border rounded-md p-3 ">
      <div class="text-2xl text-center font-bold">
      <Icon name="entypo:login"/>
        เข้าสู่ระบบ
      </div>

      <label class="form-control w-full">
        <div class="label">
          <span class="label-text">ชื่อผู้ใช้</span>
        </div>
        <input v-model="loginForm.username" type="text" placeholder="ชื่อผู้ใช้" class="input input-bordered w-full" />
      </label>


      <label class="form-control w-full">
        <div class="label">
          <span class="label-text">รหัสผ่าน</span>
        </div>
        <input :class="{ 'input-error': hasErrors.username }" v-model="loginForm.password" type="password"
          placeholder="รหัสผ่าน" class="input input-bordered w-full" />

        <div class="label">
          <span v-show="hasErrors.username" class="label-text-alt text-error">{{ hasErrors.username }}</span>
        </div>

      </label>

      <button @click="login" className="btn btn-block mt-3 bg-sky-500 text-white text-xl font-bold">เข้าสู่ระบบ</button>
    </div>

    <dialog ref="alertModal" id="my_modal_3" class="modal">
      <div class="modal-box">

        <h3 class="font-bold text-lg">แจ้งเตือน</h3>
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
  let result = await useFetch("http://localhost:8000/api/method/login",{
    method : "post",
    credentials : "include",
    body : {
      usr : loginForm.username,
      pwd : loginForm.password
    }
  })

  console.log(result)
  loginSuccess = result.status.value === "success"


  if (loginSuccess) {
    router.push({ path: '/home' })
  } else {
    alertModal.value?.showModal()
    


    hasErrors.message = result.error.value?.data?.message
  }
}
</script>

<style></style>