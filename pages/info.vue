<template>
    <div class="flex h-dvh">
        <div class=" w-full ">
            <div class="pt-2 text-xl">
                <Icon name="ep:back"></Icon>
            </div>

            <div class="text-2xl text-center font-bold">
                ข้อมูลผู้ใช้น้ำ
                <Icon name="mdi:account" />
            </div>
            <div class="m-3">
                <div class="m-3 p-2 border rounded-md border-sky-500">
                    <p><b>ชื่อผู้ใช้น้ำ</b> นายสมชาย แมนมาก</p>
                    <p><b>ที่อยู่</b> 389 ม.3 อ.เมือง จ.พะเยา</p>
                    <p><b>หมายเลขมิเตอร์ประจำเดือน</b> 789</p>
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
            <button class="btn btn-block mt-3 bg-sky-500 text-white text-xl font-bold">เพิ่มบิลการใช้น้ำ
                <icon name="icon-park-outline:bill" /></button>








        </div>
    </div>
</template>