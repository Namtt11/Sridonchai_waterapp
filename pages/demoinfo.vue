<template>
    <div>
      <!-- <v-spinner v-if="data.value === null"></v-spinner> -->
      
      <div v-for="(user,index) in users" :key="index">
        <p><b>ชื่อผู้ใช้น้ำ</b> {{ user.ownerName }}</p>
        <p><b>ที่อยู่</b> {{ user.address }}</p>
        
        <table class="table table-zebra">
          <thead>
            <tr>
              <th>เดือน</th>
              <th>จำนวนการใช้น้ำ (หน่วย)</th>
              <th>ยอดชำระ (บาท)</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(usage, i) in user.usages" :key="i">
              <td>{{ usage.month }}</td>
              <td>{{ usage.totalUnit }}</td>
              <td>{{ usage.totalPrice }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      
      <!-- <div v-else-if="error.value">
        <p>เกิดข้อผิดพลาด: {{ error.value.message }}</p>
      </div> -->
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  import { useRouter } from 'vue-router';
  
  interface User {
    ownerName: string;
    address: string;
    totalPrice: number;
    meterNumber: string;
    usages: Usage[];
  }
  
  interface Usage {
    month: string;
    totalUnit: number;
    totalPrice: number;
  }
  
  
  const users = ref<User[]>([]);
  const router = useRouter();
  
  
  
//   const isValidUser = (obj: any): obj is User => (
//     typeof obj.ownerName === 'string' &&
//     typeof obj.address === 'string' &&
//     typeof obj.totalPrice === 'number' &&
//     typeof obj.meterNumber === 'string' &&
//     Array.isArray(obj.usages) &&
//     obj.usages.every(isValidUsage)
//   );
  
//   const isValidUsage = (obj: any): obj is Usage => (
//     typeof obj.month === 'string' &&
//     typeof obj.totalUnit === 'number' &&
//     typeof obj.totalPrice === 'number'
//   );
  </script>
  