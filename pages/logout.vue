<template>
  <div class="flex h-dvh">
    <div class="my-auto w-full mx-3 border rounded-md p-3 ">
      <div class="text-2xl text-center font-bold text-red-500" >
      <Icon name="entypo:login"/>
        ออกจากระบบ
        <div>คุณต้องการจะออกจากระบบใช่หรือไม่</div>
      </div>

      

      <button @click="yes" className="btn btn-block mt-3 bg-green-500 text-white text-xl font-bold">ใช่</button>
      <button @click="no" className="btn btn-block mt-3 bg-red-500 text-white text-xl font-bold">ไม่ใช่</button>
    </div>
  </div>
</template>

<script lang="ts" setup>

// import { defineComponent } from '@nuxt/types';
// export default defineComponent({
//   methods: {
//     redirectToNextPage() {
//       this.$router.push('/next-page');
//     }
//   }
// });

const router = useRouter()


async function  yes() {
 
  let loginSuccess = false;
  let result = await useFetch("http://localhost:8000/api/method/logout",{
    method : "post",
    credentials : "include",
  
  })

  console.log(result)
  loginSuccess = result.status.value === "success"


  if (loginSuccess) {
    router.push({ path: '/login' })
  } 
};
async function  no() {
  router.push({ path: '/home' })
}

</script>

<style></style>