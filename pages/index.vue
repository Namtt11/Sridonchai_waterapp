<template>
  <div class="flex h-screen">
    <div class="my-auto w-full mx-3 border rounded-md p-3 ">
      <div class="text-2xl text-center font-bold">Login</div>

      <label class="form-control w-full">
        <div class="label">
          <span class="label-text">Username</span>
        </div>
        <input type="text" placeholder="Username" class="input input-bordered w-full" />
      </label>

      <label class="form-control w-full">
        <div class="label">
          <span class="label-text">Password</span>
        </div>
        <input type="password" placeholder="Password" class="input input-bordered w-full" />
      </label>

      <button className="btn btn-block mt-3 bg-sky-500 text-white text-xl font-bold">Login</button>
    </div>


  </div>
</template>

<script lang="ts" setup>

</script>

<style></style>