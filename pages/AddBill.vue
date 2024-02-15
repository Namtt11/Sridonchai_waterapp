<template>
    <div class="flex h-dvh">
      <div class="w-full">
  
        <div class="my-6 text-2xl text-center rounded-md border-sky-500">เพิ่มการใช้น้ำเดือน</div>
  
        <div class="text-center">ข้อมูลการใช้น้ำย้อนหลัง <Icon name="ion:water-outline" /></div>
  
        <div class="overflow-x-auto">
          <table class="table table-zebra">
            <!-- head -->
            <thead>
              <tr>
                <th>เดือน</th>
                <th>จำนวนการใช้น้ำ (หน่วย)</th>
                <th>ยอดชำระ (บาท)</th>
              </tr>
            </thead>
            <tbody>
              <!-- rows -->
              <tr v-for="(row, index) in rows" :key="index">
                <td>{{ row.month }}</td>
                <td>{{ row.waterUsage }}</td>
                <td>{{ row.payment }}</td>
              </tr>
            </tbody>
          </table>
        </div>
  
        <div class="mt-3 text-center text-xl">กรอกข้อมูลปัจจุบัน</div>
  
        <!-- Current Meter -->
        <div class="mt-3 flex space-x-10 justify-center">
          <div class="mx-3 justify-start">เลขมิเตอร์ปัจจุบัน</div>
          <div><input v-model="currentMeter" type="text" placeholder="0" class="input input-bordered input-primary w-24 max-w-xs" /></div>
          <div class="mr-3">หน่วย</div>
        </div>
  
        <!-- Price -->
        <div class="mt-4 flex space-x-10 justify-center">
          <div class="mx-3 justify-start">ราคา</div>
          <div><input v-model="price" type="text" placeholder="0" class="input input-bordered input-primary w-24 max-w-xs" /></div>
          <div class="mr-3">บาท</div>
        </div>
  
        <!-- Buttons -->
        <div class="mt-3 flex space-x-10 justify-center">
          <div> <button class="btn btn-error" @click="Cancel">ยกเลิก</button></div>
          <div><button class="btn btn-success">บันทึก</button></div>
        </div>
  
      </div>
    </div>
  </template>
  
  <script setup lang="ts">

  import { ref } from 'vue';
  
  const month = ref({
    month: new Date().getMonth(),
    year: new Date().getFullYear()
  });
  
  const currentMeter = ref('');
  const price = ref('');
  
  const rows = ref([
    { month: 'มกราคม', waterUsage: 20, payment: 140 },
    { month: 'ธันวาคม', waterUsage: 15, payment: 105 },
    { month: 'พฤษจิกายน', waterUsage: 17, payment: 119 },
  ]);


  const router = useRouter()
  async function  Cancel() {
  router.push({ path: '/info' })
}
  </script>
  