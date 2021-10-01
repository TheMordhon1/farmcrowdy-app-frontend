<template lang="">
  <div class="success-page">
    <div class="container mx-auto h-screen flex justify-center items-center">
      <div class="w-full lg:w-1/3 px-10 lg:px-0">
        <div class="flex justify-center items-center mx-auto mb-8">
          <img src="/funding-sukses.png" alt="" class="w-2/3" />
        </div>
        <h1 class="font-medium mb-3 text-2xl text-center">
          Terimakasih, Orang Baik !
        </h1>
        <p class="text-center font-light">
          Dana akan diserahkan jika sudah <br />
          <b class="font-bold">terkumpul sebanyak 75%</b> dari total dana yang
          dibutuhkan.
        </p>
        <div class="mb-3 mt-3">
          <a
            href="/semua-proyek"
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
            Bantu Projek Lainnya
          </a>
        </div>
        <div class="mb-10">
          <a
            href="/dashboard/transaksi"
            class="
              block
              w-full
              btn-redirect-blue
              border border-gray-500
              text-gray-500
              font-light
              px-6
              py-4
              text-lg
              rounded-full
              text-center
            "
          >
            Lihat Dashboard
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
