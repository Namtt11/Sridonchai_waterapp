<template>
    <div class="flex h-dvh">
        <div class="my-auto w-full mx-3 border rounded-md p-3 ">
            <div class="text-2xl text-center font-bold">
            รับชำระเงิน
            </div>
            <div class="overflow-y-auto mt-3 h-full">
      <div class="grid gap-2">
        <div
        @click="GoInfo(data.name)"
          v-bind:key="data.name"
          v-for="data in combinedData"
          class="flex-col border-solid border-2 border-gray-300 p-3">
          <div class="text-md font-bold">2023-11</div>
          <span class="align-text-bottom">
            <span>สถานะ : ยังไม่ได้เก็บเงิน</span>
          </span>
        </div>
      </div>
    </div>
        </div>
    </div>
   
           
</template>

<script lang="ts" setup>


const route = useRoute()
console.log(route.params)
const waterusage = route.params.waterusage

const axios = require('axios');

const url = 'http://localhost:8000/api/resource/Water Usage';
const params = {
  fields: JSON.stringify(["date_recieve", "name", "month"]),
  filters: JSON.stringify([["date_recieve", "is", "not set"], ["house", "=", "143 - อ.ทวีศักดิ์  รักษาศรี"]])
};

const res =  axios.get('http://localhost:8000/api/resource/Water Usage', { params });

console.log(res.data); // คุณสามารถทำอะไรกับข้อมูลที่ได้จากการรับคำตอบได้ต่อไป
const router = useRouter();
async function GoInfo(id: string) {
  router.push({ path: '/info/' + id });
}
</script>