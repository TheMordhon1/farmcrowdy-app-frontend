<template lang="">
  <footer class="py-20 text-white text-lg relative z-0">
    <section class="call-to-action  lg:mb-40 mb-20">
      <div class="container mx-auto">
        <div class="w-full text-center">
          <h1 class="text-3xl lg:text-5xl text-white font-semibold">
            Membantu Petani
            <br />
            untuk Maju
          </h1>
          
          <button
          v-if="this.$store.state.auth.loggedIn"
            @click="$router.push({ path: '/semua-proyek' })"
            class="
              inline-block
              bg-button
              text-white
              font-semibold
              px-6
              py-4
              mt-8
              text-lg
              rounded-full
            "
          >
            Mulai Sekarang
          </button>
          <button
          v-else
            @click="$router.push({ path: '/login' })"
            class="
              inline-block
              bg-button
              text-white
              font-semibold
              px-6
              py-4
              mt-8
              text-lg
              rounded-full
            "
          >
            Mulai Sekarang
          </button>
        </div>
      </div>
    </section>
    <div class="container px-5 md:px-0 mx-auto">
      <div class="sm:flex mb-4">
        <div class="sm:w-1/2 sm:mt-0 mt-8 h-auto">
          <img src="logo@2x.png" alt="" class="mb-3" />
          <p class="font-light">Membantu Petani<br />Dapat Akses Permodalan</p>
        </div>
        <div class="sm:w-1/4 h-auto">
          <div class="mb-5 mt-8 font-bold">Jelajahi</div>
          <ul class="font-light">
            <li class="mb-3">Layanan Kami</li>
            <li class="mb-3">Sistem</li>
            <li class="mb-3">Pengembalian</li>
            <li class="mb-3">Bagi Hasil</li>
          </ul>
        </div>
        <div class="sm:w-1/4 h-auto">
          <div class="mb-5 mt-8 font-bold">Investor</div>
          <ul class="font-light">
            <li class="mb-3">Akun Saya</li>
            <li class="mb-3">Top Startups</li>
            <li class="mb-3">Panduan</li>
            <li class="mb-3">Saldo</li>
          </ul>
        </div>
        <div class="sm:w-1/4 h-auto">
          <div class="mb-5 mt-8 font-bold">Kontak Kami</div>
          <ul class="font-light">
            <li class="mb-3">+021 2208 1996</li>
            <li class="mb-3">Bantarjati, Bogor Utara</li>
            <li class="mb-3">Kota Bogor</li>
            <li class="mb-3">support@farmcrowdy.id</li>
          </ul>
        </div>
      </div>
      <img class="leafs-footer-img" src="/leafs.png"></img>
    </div>
  </footer>
</template>
<script>
export default {};
</script>
<style lang=""></style>
