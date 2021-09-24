<template lang="">
  <div class="container mx-auto h-screen flex justify-center items-center">
    <div class="w-full lg:w-1/4 px-10 lg:px-0 py-10">
      <div class="flex justify-center items-center mx-auto mt-6 mb-8">
        <img src="/success-illustration.png" alt="" class="w-full" />
      </div>
      <h2 class="font-medium mb-3 text-3xl text-center">Berhasil :)</h2>
      <p class="text-center font-light">
        Waw, foto profil anda berhasil terubah
      </p>
      <div class="mb-4 mt-6">
        <div class="mb-3">
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
            Kembali Jelajahi
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
