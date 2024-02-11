<template>
    <div class="flex h-dvh">
        <div class="my-auto w-full mx-3 border rounded-md p-3 ">
            <div class="text-2xl text-center font-bold">
           
            สรุปยอด
            </div>
            
      <button @click="Yes" className="btn btn-block mt-3 bg-green-500 text-white text-xl font-bold">ยืนยัน</button>
      <button @click="No" className="btn btn-block mt-3 bg-red-500 text-white text-xl font-bold">ยกเลิก</button>
        </div>
    </div>
   
           
</template>

<script>
export default {
  methods: {
    Yes() {
      this.$router.push('/total');
      
    },
    No() {
      this.$router.push('/Addbill');
    }
}
}
</script>