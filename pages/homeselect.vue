<template>
  <div class="flex h-dvh">
    <div class="w-full">
      <div class="flex items-stretch gap-3 p-3 mx-3">
        <div @click="Back"><Icon name="mdi:arrow-back-circle" size="36"/></div>
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
          <p><b>ชื่อผู้ใช้น้ำ</b> {{ user.ownerName }}</p>
          <p><b>ที่อยู่</b> {{ user.address }}</p>
          <p><b>ค้างชำระ</b> {{ user.totalPrice }} บาท</p>
          <p><b>หมายเลขมิเตอร์ประจำเดือน</b> {{ user.meterNumber }}</p>
          <div v-for="(usage, i) in user.usages" :key="i">
            <p><b>เดือน</b> {{ usage.month }}</p>
            <p><b>จำนวนหน่วย</b> {{ usage.totalUnit }}</p>
            <p><b>ราคารวม</b> {{ usage.totalPrice }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';

// Interface for the User data type
interface User {
  ownerName: string;
  address: string;
  totalPrice: number;
  meterNumber: string;
  usages: Usage[];
}

// Interface for the Usage data type
interface Usage {
  month: string;
  totalUnit: number;
  totalPrice: number;
}

// Reactive property to store the search query
const searchQuery = ref('');

// Reactive property to store the user data
const users = ref<User[]>([]);

// Router instance
const router = useRouter();

// Fetch user data and assign it to the `users` array
const search = async () => {
  try {
    const response = await fetch('/api/get_info_house', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({ searchQuery: searchQuery.value })
    });

    if (!response.ok) {
      throw new Error('Failed to fetch data');
    }

    const data = await response.json();

    // Handle potential inconsistencies in response structure
    if (!Array.isArray(data) || !data.every((d: any) => isValidUser(d))) {
      throw new Error('Invalid API response format');
    }

    // Cast the response data to the User type
    users.value = data as User[];
  } catch (error) {
    console.error(error);
    // Handle errors gracefully, e.g., display user-friendly messages
  }
};

// Function to validate if an object is a valid User
function isValidUser(obj: any): obj is User {
  return (
    typeof obj.ownerName === 'string' &&
    typeof obj.address === 'string' &&
    typeof obj.totalPrice === 'number' &&
    typeof obj.meterNumber === 'string' &&
    Array.isArray(obj.usages) &&
    obj.usages.every((usage: any) => isValidUsage(usage))
  );
}

// Function to validate if an object is a valid Usage
function isValidUsage(obj: any): obj is Usage {
  return (
    typeof obj.month === 'string' &&
    typeof obj.totalUnit === 'number' &&
    typeof obj.totalPrice === 'number'
  );
}

// Navigate back to the home page
async function Back() {
  await router.push({ path: '/home'});
}
</script>
