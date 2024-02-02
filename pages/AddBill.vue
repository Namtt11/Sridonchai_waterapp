<template>
    <div class="flex h-dvh">
    <div class=" w-full ">

        <div class=" my-6 text-2xl text-center rounded-md border-sky-500">เพิ่มการใช้น้ำเดือน</div>
        <div class="  text-center">ข้อมูลการใช้น้ำย้อนหลัง <Icon name="ion:water-outline"/></div>
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
                    <!-- row 1 -->
                    <tr>
                        <td>มกราคม</td>
                        <td>20</td>
                        <td>140</td>
                    </tr>
                    <!-- row 2 -->
                    <tr>
                        <td>ธันวาคม</td>
                        <td>15</td>
                        <td>105</td>
                    </tr>
                    <!-- row 3 -->
                    <tr>
                        <td>พฤษจิกายน</td>
                        <td>17</td>
                        <td>119</td>
                    </tr>
                </tbody>
            </table>
        </div>
        <div class="mt-3 text-center text-xl">กรอกข้อมูลปัจจุบัน</div>
        <div class="mt-3 flex space-x-10  justify-center">
            <div class="mx-3 justify-start">เลขมิเตอร์ปัจจุบัน</div>
            <div><input type="text" placeholder="0" class="input input-bordered input-primary w-24 max-w-xs" /></div>
            <div class="mr-3">หน่วย</div>
        </div>
        <div class="mt-3 flex space-x-10  justify-center">
            <div class="mx-3 justify-start">ราคา</div>
            <div><input type="text" placeholder="0" class="input input-bordered input-primary w-24 max-w-xs" /></div>
            <div class="mr-3">บาท</div>
        </div>
        
        <div class="mt-3 flex space-x-10 justify-center">
            <div> <button class="btn btn-error">ยกเลิก</button></div>
            <div><button class="btn btn-success">บันทึก</button></div>
        </div>
        

        
    
    </div>
   </div>      
</template>
<script setup lang="ts">
import VueDatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css'
import { ref } from 'vue';

const month = ref({
    month: new Date().getMonth(),
    year: new Date().getFullYear()
});
</script>