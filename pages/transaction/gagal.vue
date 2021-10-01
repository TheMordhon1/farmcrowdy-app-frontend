<template lang="">
  <div class="success-page">
    <div class="container mx-auto h-screen flex justify-center items-center">
      <div class="w-full lg:w-1/3 px-10 lg:px-0">
        <div class="flex justify-center items-center mx-auto mb-8">
          <img src="/funding-gagal.png" alt="" class="w-2/3" />
        </div>
        <h1 class="font-medium mb-3 text-2xl text-center">
          Transaksi Tidak Berhasil!
        </h1>
        <p class="text-center font-light">Pastikan anda mengikuti anjuran.</p>
        <div class="mb-10 mt-5">
          <a
            href="/dashboard/transaksi"
            class="
              block
              w-full
              bg-button-rounded
              text-white
              font-semibold
              px-6
              py-4
              text-lg
              rounded-full
              text-center
            "
          >
            Ulangi
          </a>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  layout: "success",
};
</script>
