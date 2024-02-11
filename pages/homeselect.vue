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
  
  <!-- <script setup lang="ts">
  const searchQuery = ref('');
  import VueDatePicker from "@vuepic/vue-datepicker";
import "@vuepic/vue-datepicker/dist/main.css";
import { ref } from "vue";
import { type ReportHouse } from "@/domains/types/reportHouse";

const month = ref({
  month: new Date().getMonth(),
  year: new Date().getFullYear(),
});

const selectedDate = () => {
  console.log(month);
  console.log(month.value.year);
  let curMonth = ("0000000000" + (month.value.month + 1)).slice(-2);
  console.log(curMonth);

  let resultMonth = month.value.year + "-" + curMonth;
  console.log(resultMonth);

  loadReportHouse(resultMonth)
};

function backgroundColor(status: string) {
  if (status === "เก็บเงินแล้ว") {
    return "bg-green-100";
  } else if (status === "จดมิเตอร์แล้ว") {
    return "bg-yellow-100";
  } else {
    return "bg-red-100";
  }
}

function textColor(status: string) {
  if (status === "เก็บเงินแล้ว") {
    return "text-green-500";
  } else if (status === "จดมิเตอร์แล้ว") {
    return "text-yellow-500";
  } else {
    return "text-red-500";
  }
}

const statusFilter = ["เก็บเงินแล้ว", "จดมิเตอร์แล้ว", "ยังไม่ได้ดำเนินการ"];

const selectedStatus = ref([
  "เก็บเงินแล้ว",
  "จดมิเตอร์แล้ว",
  "ยังไม่ได้ดำเนินการ",
]);

function toggleSelectedStatus(status: string) {
  if (selectedStatus.value.find((x: string) => x === status)) {
    selectedStatus.value.splice(selectedStatus.value.indexOf(status), 1);
  } else {
    selectedStatus.value.push(status);
  }
}

function toggleStatus(status: string) {
  if (selectedStatus.value.find((x: string) => x === status)) {
    return ["bg-green-200", "text-black"];
  } else {
    return "bg-gray-200";
  }
}

// const reportData = ref(result.data.value?.message);
const reportData = ref([] as ReportHouse[]);

const loadReportHouse = async (sel_month : string) => {
  let result = await useFetch<{ message: ReportHouse[] }>(
    "http://localhost:8000/api/method/sridonchai.sridonchai.api.get_house_status_by_month",
    {
      method: "post",
      body: {
        month: sel_month,
      },
    }
  );

  reportData.value = result.data.value?.message ?? []
};

selectedDate()

const reportFilteredData = computed(() => {
  return reportData?.value?.filter((x: ReportHouse) =>
    selectedStatus.value.find((s: string) => s === x.status)
  );
});
  
  const search = () => {
    // Implement your search logic here
    // You can filter the 'users' array based on the searchQuery
  };
  </script>
  