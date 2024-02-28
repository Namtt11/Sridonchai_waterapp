<template>
    <div class="flex h-dvh">
        <div class="my-auto w-full mx-3 border rounded-md p-3 ">
            <div class="text-2xl text-center font-bold">
            รับชำระเงิน
            </div>
            <div class="overflow-y-auto mt-3 h-full">
      <div class="grid gap-2">
        <div
          class="flex-col border-solid border-2 border-gray-300 p-3" >
          <div class="text-md font-bold" @click="Paybill">2023-11</div>
          <span class="align-text-bottom">
            <span>สถานะ : ยังไม่ได้เก็บเงิน</span>
          </span>
        </div>
      </div>
    </div>
        </div>
    </div>
   
           
</template>

<script>
const router = useRouter();
async function  Paybill() {
router.push({ path: '/getmonney/' })
}

</script>