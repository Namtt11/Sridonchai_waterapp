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
            <div class="  grid gap-2 mt-3">
                <div class="flex-col border-solid border-2 border-gray-300 p-3 bg-green-100 ">
                    <div class="text-lg font-bold"> นายป่านฟ้า จตุรคเชนทร์เดชา</div>
                    <div> 221/1 ม.2 ต.เวียง อ.เชียงของ จ.เชียงราย</div>
                    <div class="flex  align-bottom "><div class=" inline-block align-bottom"> สถานะ</div><div class="ml-1 text-green-500 text-lg font-bold ">เก็บเงินแล้ว</div>
                    <span class="inline-block align-bottom ">aaaaaa</span>
                    </div>
                </div>
                <div class="flex-col border-solid border-2  border-gray-300 p-3 ">
                    <div>ชื่อ นายณัฐพล ดิษฐ์สิริ </div>
                    <div>ที่อยู่ 2 ม.2 ต.เวียง อ.เชียงของ จ.เชียงราย </div>
                    <div class="flex">สถานะ<div class="ml-1 text-yellow-500">จดมิเตอร์แล้ว</div>
                    </div>
                </div>
                <div class="flex-col border-solid border-2  border-gray-300 p-3">
                    <div>ชื่อ นายกิตติ ผิวนวล </div>
                    <div>ที่อยู่ 31 ม.2 ต.เวียง อ.เชียงของ จ.เชียงราย </div>
                    <div class="flex">สถานะ<div class="ml-1 text-red-500">ยังไม่ได้ดำเนินการ</div>
                    </div>
                </div>
                <div class="flex-col border-solid border-2 border-gray-300 p-3 ">
                    <div>ชื่อ นายป่านฟ้า จตุรคเชนทร์เดชา</div>
                    <div>ที่อยู่ 221/1 ม.2 ต.เวียง อ.เชียงของ จ.เชียงราย</div>
                    <div class="flex">สถานะ<div class="ml-1 text-green-500">เก็บเงินแล้ว</div>
                    </div>
                </div>



            </div>
            <div class="btm-nav">
                <button>
                    <icon class="h-6 w-6" name="material-symbols:home"/>
                    <span class="btm-nav-label">Home</span>
                </button>
                <button class="active">
                    <icon class="h-6 w-6" name="material-symbols:table"/>
                    <span class="btm-nav-label">Home Select</span>
                </button>
                <button>
                    <icon class="h-6 w-6" name="mdi:user"/>
                    <span class="btm-nav-label">User</span>
                </button>
            </div>

        </div>

    </div>
</template>
<script>
    import VueDatePicker from '@vuepic/vue-datepicker';
    import '@vuepic/vue-datepicker/dist/main.css'
    import {
        ref
    } from 'vue';
    const month = ref({
        month: new Date().getMonth(),
        year: new Date().getFullYear()
    });

    export default {
        components: {
            VueDatePicker
        },
        data() {
            return {
                date: null,
            };
        }
    }
</script>