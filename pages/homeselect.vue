<template>
    <div class="flex h-dvh">
      <div class="w-full">
        <div class="flex items-stretch gap-3 p-3 mx-3">
          <input
            v-model="searchQuery"
            type="text"
            placeholder="ค้นหาบ้าน"
            class="input input-bordered w-full max-w-xs border-sky-500"
          />
          <button @click="search" class="btn flex-col bg-white border-sky-500">
            ค้นหา
          </button>
        </div>
        <div class="m-3">
          <div v-for="(user, index) in users" :key="index" class="m-3 p-3 border rounded-md border-sky-500">
            <p><b>ชื่อผู้ใช้น้ำ</b> {{ user.name }}</p>
            <p><b>ที่อยู่</b> {{ user.address }}</p>
            <p><b>ค้างชำระ</b> {{ user.amount }} บาท</p>
            <p><b>หมายเลขมิเตอร์ประจำเดือน</b> {{ user.meterNumber }}</p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  const searchQuery = ref('');
  const users = ref([
    {
      name: 'นายสมชาย แมนมาก',
      address: '389 ม.3 อ.เมือง จ.พะเยา',
      amount: 100,
      meterNumber: 789,
    },
    {
      name: 'นายสม หมา',
      address: '389 ม.3 อ.เมือง จ.พะเยา',
      amount: 100,
      meterNumber: 789,
    },
    // Add more user data as needed
  ]);
  
  const search = () => {
    // Implement your search logic here
    // You can filter the 'users' array based on the searchQuery
  };
  </script>
  