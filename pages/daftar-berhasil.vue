<template lang="">
  <div class="container mx-auto h-screen flex justify-center items-center">
    <div class="w-full lg:w-1/3 px-10 lg:px-0">
      <div class="flex justify-center items-center mx-auto mb-8">
        <img src="/success-illustration.png" alt="" class="w-full" />
      </div>
      <h2 class="font-medium mb-3 text-3xl text-center">Selamat Datang!</h2>
      <p class="text-center font-light">
        Akun Anda Berhasil Terdaftar
        <br />
        Ke Dalam Sistem
      </p>
      <div class="mb-10 mt-6">
        <a
          href="/"
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
          Mulai Jelajahi
        </a>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  layout: "success",
};
</script>
