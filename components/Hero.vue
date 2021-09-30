<template lang="">
  <section class="landing-hero pt-5">
    <div class="header__bg"></div>
    <div class="container mx-auto relative">
      <Navbar />
      <div class="flex flex-col items-center pt-10 px-5 md:px-0 lg:flex-row">
        <div class="lg:hidden block lg:w-1/2 flex justify-center mt-5 lg:mt-0">
          <img src="hero-image@2x.png" alt="crowdfunding project" />
        </div>
        <div class="w-full lg:w-1/2">
          <h1
            class="
              text-center
              lg:text-left
              text-2xl
              lg:text-4xl
              text-white
              mb-5
            "
          >
            Platform Untuk Membantu<u class="hero-underline"> Petani</u>
            Mendapatkan<u class="hero-underline"> Akses Permodalan </u>
          </h1>

          <p
            class="text-center lg:text-left text-white text-xl font-light mb-8"
          >
            Mendanai proyek yang terbaik untuk mewujudkan mimpi mereka
          </p>
          <nuxt-link
            to="/semua-proyek"
            class="
              block
              bg-button-rounded
              lg:bg-button
              text-white
              font-semibold
              px-12
              py-3
              text-xl text-center
              w-full
              lg:w-1/2
            "
          >
            Temukan Proyek
          </nuxt-link>
        </div>
        <div class="hidden lg:block lg:w-1/2 flex justify-center mt-5 lg:mt-0">
          <img src="hero-image@2x.png" alt="crowdfunding project" />
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {};
</script>
<style lang=""></style>
