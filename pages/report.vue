<template>
    <div class="flex h-dvh w-full">
        <div class="w-full p-3 mx-3 ">
            <VueDatePicker v-model="month" month-picker />
            <div class="mt-3 ">
                <select class="select select-bordered w-full ">
                    <option disabled selected>เลือกผู้ใช้น้ำ</option>
                    <option>นายปฎิภาณ ศักดิ์ดา</option>
                    <option>นางสาวโทนี่ กิม</option>
                </select>
            </div>
            <div class="mt-3 flex flex-col items-center    ">
                <div class="radial-progress text-sky-500 mx-auto" style="--value:70;--size:128px;" role="progressbar ">
                    70%</div>

            </div>
            <div class="grid gap-2 mt-3">

                <div v-for="data in reportData" :class="[backgroundColor(data.status)]"
                    class="flex-col border-solid border-2 border-gray-300 p-3">
                    <div class="text-lg font-bold">{{ data.name }}</div>
                    <div> {{ data.address }}</div>
                    <span class="align-text-bottom">
                        <span>สถานะ</span>
                        <span :class="[textColor(data.status)]" class="ml-1 text-lg font-bold ">{{ data.status }}</span>
                    </span>
                </div>

            </div>
            <div class="btm-nav">
                <button>
                    <icon class="h-6 w-6" name="material-symbols:home" />
                    <span class="btm-nav-label">Home</span>
                </button>
                <button class="active">
                    <icon class="h-6 w-6" name="material-symbols:table" />
                    <span class="btm-nav-label">Home Select</span>
                </button>
                <button>
                    <icon class="h-6 w-6" name="mdi:user" />
                    <span class="btm-nav-label">User</span>
                </button>
            </div>

        </div>

    </div>
</template>
<script setup lang="ts">
import VueDatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css'
import { ref } from 'vue';
import {ReportType} from "@/domains/types/types.ts";
const month = ref({
    month: new Date().getMonth(),
    year: new Date().getFullYear()
});



function backgroundColor(status: string) {
    if (status === "เก็บเงินแล้ว") {
        return "bg-green-100"
    } else if (status === "จดมิเตอร์แล้ว") {
        return "bg-yellow-100"
    } else {
        return "bg-red-100"
    }
}

function textColor(status: string) {
    if (status === "เก็บเงินแล้ว") {
        return "text-green-500"
    } else if (status === "จดมิเตอร์แล้ว") {
        return "text-yellow-500"
    } else {
        return "text-red-500"
    }
}

const reportData = ref([
    { name: "ป่านฟ้า", address: "221/1", status: "เก็บเงินแล้ว" },
    { name: "ป่านฟ้า", address: "221/1", status: "จดมิเตอร์แล้ว" },
    { name: "ป่านฟ้า", address: "221/1", status: "ยังไม่ได้ดำเนินการ" },
] as ReportHouse[])

</script>