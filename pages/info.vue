<template>
    <div class="flex flex-col mx-3 h-dvh relative">
        <div class="flex flex-col sticky top-0 pt-3 bg-white">
        
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
                        <!-- row 4 -->
                        <tr>
                            <td>ตุลาคม</td>
                            <td>17</td>
                            <td>119</td>
                        </tr>
                        <!-- row 5 -->
                        <tr>
                            <td>กันยายน</td>
                            <td>17</td>
                            <td>119</td>
                        </tr>
                        <!-- row 6 -->
                        <tr>
                            <td>สิงหาคม</td>
                            <td>17</td>
                            <td>119</td>
                        </tr>
                        <!-- row 7 -->
                        <tr>
                            <td>กรกฎาคม</td>
                            <td>17</td>
                            <td>119</td>
                            <!-- row 8 -->
                        <tr>
                            <td>มิถุนายน</td>
                            <td>17</td>
                            <td>119</td>
                        </tr>
                        <!-- row 9 -->
                        <tr>
                            <td>พฤษภาคม</td>
                            <td>17</td>
                            <td>119</td>
                        </tr>
                        <!-- row 10 -->
                        <tr>
                            <td>เมษายน</td>
                            <td>17</td>
                            <td>119</td>
                        </tr>
                        <!-- row 11 -->
                        <tr>
                            <td>มีนาคม</td>
                            <td>17</td>
                            <td>119</td>
                        </tr>
                        <!-- row 12 -->
                        <tr>
                            <td>กุมภาพันธ์</td>
                            <td>17</td>
                            <td>119</td>
                        </tr>
                        </tr>
                    </tbody>
                </table>
            </div>
            <button class="btn btn-block mt-3 bg-sky-500 text-white text-xl font-bold">เพิ่มบิลการใช้น้ำ
                <icon name="icon-park-outline:bill" /></button>


        </div>
    </div>
</template>