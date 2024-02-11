<template>
    <div class="flex flex-col mx-3 h-dvh relative">
      <div class="flex flex-col sticky top-0 pt-3 bg-white">
        <div @click="Back"><Icon name="mdi:arrow-back-circle" size="36"/></div>
        <div class="text-2xl text-center font-bold">
          ข้อมูลผู้ใช้น้ำ
          <Icon name="mdi:account" />
        </div>
        
        <div class="m-3">
          <div class="m-3 p-2 border rounded-md border-sky-500">
            <p><b>ชื่อผู้ใช้น้ำ</b> นายสมชาย แมนมาก</p>
            <p><b>ที่อยู่</b> 389 ม.3 อ.เมือง จ.พะเยา</p>
          </div>
        </div>
  
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
  
        <button class="btn btn-block mt-3 bg-sky-500 text-white text-xl font-bold" @click="NextPageAddbill">
          เพิ่มบิลการใช้น้ำ
          <icon name="icon-park-outline:bill" />
        </button>
  
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        rows: [
          { month: 'มกราคม', waterUsage: 20, payment: 140 },
          { month: 'ธันวาคม', waterUsage: 15, payment: 105 },
          // เพิ่มเดือนและข้อมูลตามต้องการ
        ]
      };
    },
    methods: {
    NextPageAddbill() {
      this.$router.push('/Addbill'); 
    },
    Back() {
      this.$router.push('/homeselect'); 
    }
  },
    

  }
  </script>
  