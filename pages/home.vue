<template>
    <div>
      <div>
      </div>
    </div>
    <div>
      <div class="card w-80 pt-6 mx-8 bg-base-80 shadow-xl image-full">
  <figure><img src="https://www.scb.co.th/content/scb/th/personal-banking/stories/tips-for-you/pdpa-about-us/jcr:content/par/wrappercomp/wrapper/rowcomp/col-1/storyinfocomp/par/image.img.jpg/1588856853514.jpg" alt="Shoes" /></figure>
  <div class="card-body">
    <h2 class="card-title">ข้อมูลส่วนตัว</h2>
    <p>เข้าเพื่อดูข้อมูลส่วนตัวของคุณ</p>
    <div class="card-actions justify-end">
      <button class="btn btn-primary" @click="NextPageMyprofile">ถัดไป</button>

    </div>
  </div>
</div>
    </div>
   
  
    <div>
        <div class="card w-80 pt-2 mx-8 bg-base-80 shadow-xl image-full">
  <figure><img src="https://s359.kapook.com/pagebuilder/7904cc36-7406-49fd-bdce-7c639fc2f4d8.jpg" alt="Shoes" /></figure>
  <div class="card-body">
    <h2 class="card-title">เลือกบ้าน</h2>
    <p>ที่คุณต้องการจะเพิ่มข้อมูลการใช้น้ำในรายเดือนนี้</p>
    <div class="card-actions justify-end">
      <button class="btn btn-primary" @click="NextPageHomeselect">ถัดไป</button>
    </div>
  </div>
</div>
<div>
  <div class="card w-80 pt-2 mx-8 bg-base-80 shadow-xl image-full">
  <figure><img src="https://ambassadorlocalmoving.com/wp-content/uploads/2020/06/pen-writing-notes-studying-1024x683.jpg"  alt="Shoes" /></figure>
  <div class="card-body">
    <h2 class="card-title">รายงาน</h2>
    <p>ดูรายงานการทำงาน</p>
    <div class="card-actions justify-end">
      <button class="btn btn-primary" @click="NextPageReport">ถัดไป</button>
    </div>
  </div>
</div>
</div>
    </div>
  <div>
    
  </div>

</template>

<script>
export default {
  methods: {
    NextPageMyprofile() {
      this.$router.push('/myprofile');
      
    },
    NextPageHomeselect() {
      this.$router.push('/homeselect');
    },
    NextPageReport() {
      this.$router.push('/report');
  }
}
}
</script>