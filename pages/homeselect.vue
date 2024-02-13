<template>
  <div class="flex h-dvh">
    <div class="w-full">
      <div class="flex items-stretch gap-3 p-3 mx-3">
        <div @click="Back"><Icon name="mdi:arrow-back-circle" size="36"/></div>
        <input
          v-model="searchInput"
          type="text"
          placeholder="ค้นหาบ้าน"
          class="input input-bordered w-full max-w-xs border-sky-500"
        />
        <button @click="search" class="btn flex-col bg-white border-sky-500">
          ค้นหา
        </button>
      </div>
      <div class="m-3">
        <VueDatePicker v-model="month" month-picker @closed="selectedDate" />
      <div class="mt-3">
        <button
          @click="toggleSelectedStatus(status)"
          :class="[toggleStatus(status)]"
          class="btn py-1 px-2 mr-2"
          v-for="status in statusFilter"
          v-bind:key="status"
        >
          {{ status }}
        </button>
      </div>
    </div>

    <div class="overflow-y-auto mt-3 h-full">
      <div class="grid gap-2">
        <div
          v-bind:key="data.name"
          v-for="data in reportFilteredData"
          :class="[backgroundColor(data.status)]"
          class="flex-col border-solid border-2 border-gray-300 p-3"
        >
          <div class="text-md font-bold">{{ data.owner_name }}</div>
          <div>{{ data.house_number }}</div>
          <span class="align-text-bottom">
            <span>สถานะ</span>
            <span
              :class="[textColor(data.status)]"
              class="ml-1 text-md font-bold"
              >{{ data.status }}</span
            >
          </span>
        </div>
      </div>
    </div>
  </div>
  </div>
</template>
<script setup lang="ts">
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
      credentials : "include",
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

const router = useRouter();
async function  Back() {
  router.push({ path: '/home' })
}


// function search(searchInputdata:string){
//   if (searchInputdata)


// }

// const reportsearchFilteredData = computed(() => {
//   return reportData?.value?.filter((x: ReportHouse) =>  
//     search.value.find((s: string) => s === x.status)
//   );
// });
 


</script>
