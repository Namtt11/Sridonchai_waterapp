<template>
  <div class="flex h-dvh">
    <div class="my-auto w-full mx-3 border rounded-md p-3 ">
      <div class="text-2xl text-center font-bold">
      <Icon name="entypo:login"/>
        Login
      </div>

      <label class="form-control w-full">
        <div class="label">
          <span class="label-text">Username</span>
        </div>
        <input v-model="loginForm.username" type="text" placeholder="Username" class="input input-bordered w-full" />
      </label>


      <label class="form-control w-full">
        <div class="label">
          <span class="label-text">Password</span>
        </div>
        <input :class="{ 'input-error': hasErrors.username }" v-model="loginForm.password" type="password"
          placeholder="Password" class="input input-bordered w-full" />

        <div class="label">
          <span v-show="hasErrors.username" class="label-text-alt text-error">{{ hasErrors.username }}</span>
        </div>

      </label>

      <button @click="login" className="btn btn-block mt-3 bg-sky-500 text-white text-xl font-bold">Login</button>
    </div>

    <dialog ref="alertModal" id="my_modal_3" class="modal">
      <div class="modal-box">

        <h3 class="font-bold text-lg">Alert</h3>
        <p class="py-4">Username or password is invalid</p>
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
  password: null
})

const alertModal = ref<HTMLDialogElement>()

const router = useRouter()

function login() {
  console.log(loginForm)
  console.log(loginForm.username, loginForm.password)

  let loginSuccess = loginForm.username == 'admin' && loginForm.password == 'pass'
  if (loginSuccess) {
    router.push({ path: '/blog' })
  } else {
    alertModal.value?.showModal()
    hasErrors.username = "Username is required"
  }
}
</script>

<style></style>