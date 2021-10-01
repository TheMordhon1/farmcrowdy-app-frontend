<template lang="">
  <div class="project-page">
    <section class="dashboard-header pt-5">
      <div class="container mx-auto relative">
        <Navbar2 />
      </div>
    </section>

    <section class="container px-5 md:px-0 mx-auto pt-8 lg:mt-10 mt-5">
      <div class="flex justify-between items-center">
        <div class="w-full mr-6">
          <h2 class="text-2xl lg:text-4xl text-gray-900 mb-2 font-medium">
            Dashboard
          </h2>
        </div>
      </div>
      <div class="flex justify-between items-center">
        <div class="w-4/4 mr-6">
          <h3 class="text-xl text-gray-900 mb-4">Buat proyek baru</h3>
        </div>
      </div>
      <v-alert
        class="info text-md lg:text-xl"
        border="top"
        colored-border
        type="info"
        elevation="2"
      >
        Berikan info yang akurat dan detail, pastikan
        <b>total biaya proyek</b> dan
        <b>yang anda tawarkan kepada funder</b>
        merupakan data yang pasti dikarenakan anda perlu
        <i>menghubungi admin</i> untuk mengubahnya.
      </v-alert>
      <div class="block mb-2">
        <div class="w-full lg:max-w-full lg:flex mb-4">
          <div
            class="
              w-full
              lg:border
              border-gray-400
              bg-white
              rounded
              lg:p-8
              flex flex-col
              justify-between
              leading-normal
            "
          >
            <form class="w-full">
              <div class="flex flex-wrap -mx-3 mb-6">
                <div class="w-full md:w-1/2 px-3 mb-6 md:mb-0">
                  <label
                    class="
                      block
                      uppercase
                      tracking-wide
                      text-gray-700 text-xs
                      font-bold
                      mb-2
                    "
                  >
                    Nama Proyek
                  </label>
                  <input
                    class="
                      appearance-none
                      block
                      w-full
                      bg-gray-200
                      text-gray-700
                      border border-gray-200
                      rounded
                      py-3
                      px-4
                      leading-tight
                      focus:outline-none focus:bg-white focus:border-gray-500
                    "
                    type="text"
                    placeholder="Projek Porang Pak Dudi"
                    v-model="campaign.name"
                  />
                </div>
                <div class="w-full md:w-1/2 px-3">
                  <label
                    class="
                      block
                      uppercase
                      tracking-wide
                      text-gray-700 text-xs
                      font-bold
                      mb-2
                    "
                  >
                    Total Biaya Proyek
                  </label>
                  <div
                    class="
                      form-nominal
                      flex
                      justify-center
                      items-center
                      relative
                    "
                  >
                    <span
                      class="
                        absolute
                        bg-gray-200
                        py-3
                        px-4
                        left-0
                        rounded
                        text-gray-700
                      "
                      >Rp</span
                    >
                    <input
                      class="
                        appearance-none
                        block
                        w-full
                        bg-gray-200
                        text-gray-700
                        border border-gray-200
                        rounded
                        py-3
                        px-4
                        leading-tight
                        focus:outline-none focus:bg-white focus:border-gray-500
                        pl-20
                      "
                      type="number"
                      min="100000"
                      step="1000000"
                      placeholder="60000000"
                      v-model.number="campaign.goal_amount"
                    />
                  </div>
                </div>
                <div class="w-full px-3">
                  <label
                    class="
                      block
                      uppercase
                      tracking-wide
                      text-gray-700 text-xs
                      font-bold
                      mb-2
                      mt-3
                    "
                  >
                    Keterangan Singkat
                  </label>
                  <input
                    class="
                      appearance-none
                      block
                      w-full
                      bg-gray-200
                      text-gray-700
                      border border-gray-200
                      rounded
                      py-3
                      px-4
                      mb-3
                      leading-tight
                      focus:outline-none focus:bg-white focus:border-gray-500
                    "
                    type="text"
                    placeholder="Deskripsi singkat mengenai projectmu"
                    v-model="campaign.short_description"
                  />
                </div>

                <div class="w-full px-3">
                  <label
                    class="
                      block
                      uppercase
                      tracking-wide
                      text-gray-700 text-xs
                      font-bold
                      mb-2
                      mt-3
                    "
                  >
                    Alamat
                  </label>
                  <input
                    class="
                      appearance-none
                      block
                      w-full
                      bg-gray-200
                      text-gray-700
                      border border-gray-200
                      rounded
                      py-3
                      px-4
                      mb-3
                      leading-tight
                      focus:outline-none focus:bg-white focus:border-gray-500
                    "
                    type="text"
                    placeholder="Kabupaten/Kota, Provinsi"
                    v-model="campaign.address"
                  />
                </div>

                <div class="w-full px-3">
                  <label
                    class="
                      block
                      uppercase
                      tracking-wide
                      text-gray-700 text-xs
                      font-bold
                      mb-2
                    "
                  >
                    Minimal Pembiayaan
                  </label>
                  <div
                    class="
                      form-nominal
                      flex
                      justify-center
                      items-center
                      relative
                    "
                  >
                    <span
                      class="
                        absolute
                        bg-gray-200
                        py-3
                        px-4
                        left-0
                        bottom-3
                        rounded
                        text-gray-700
                      "
                      >Rp</span
                    >
                    <input
                      class="
                        appearance-none
                        block
                        w-full
                        bg-gray-200
                        text-gray-700
                        border border-gray-200
                        rounded
                        py-3
                        px-4
                        leading-tight
                        focus:outline-none focus:bg-white focus:border-gray-500
                        mb-3
                        pl-20
                      "
                      min="100000"
                      step="10000"
                      type="number"
                      placeholder="100000"
                      v-model.number="campaign.min_pembayaran"
                    />
                  </div>
                </div>

                <div class="w-full px-3">
                  <label
                    class="
                      block
                      uppercase
                      tracking-wide
                      text-gray-700 text-xs
                      font-bold
                      mb-2
                    "
                  >
                    Yang anda tawarkan kepada funder
                  </label>
                  <input
                    class="
                      appearance-none
                      block
                      w-full
                      bg-gray-200
                      text-gray-700
                      border border-gray-200
                      rounded
                      py-3
                      px-4
                      mb-3
                      leading-tight
                      focus:outline-none focus:bg-white focus:border-gray-500
                    "
                    type="text"
                    placeholder="*jika lebih dari satu pisahkan dengan tanda koma (,)"
                    v-model="campaign.perks"
                  />
                </div>

                <div class="w-full px-3">
                  <label
                    class="
                      block
                      uppercase
                      tracking-wide
                      text-gray-700 text-xs
                      font-bold
                      mb-2
                    "
                  >
                    Deskripsi Komoditas
                  </label>
                  <textarea
                    rows="5"
                    class="
                      appearance-none
                      block
                      w-full
                      bg-gray-200
                      text-gray-700
                      border border-gray-200
                      rounded
                      py-3
                      px-4
                      mb-3
                      leading-tight
                      focus:outline-none focus:bg-white focus:border-gray-500
                    "
                    type="text"
                    placeholder="Komoditas proyek anda"
                    v-model="campaign.description_komoditas"
                  ></textarea>
                </div>
                <div class="w-full px-3">
                  <label
                    class="
                      block
                      uppercase
                      tracking-wide
                      text-gray-700 text-xs
                      font-bold
                      mb-2
                    "
                  >
                    Deskripsi Prospek
                  </label>
                  <textarea
                    rows="5"
                    class="
                      appearance-none
                      block
                      w-full
                      bg-gray-200
                      text-gray-700
                      border border-gray-200
                      rounded
                      py-3
                      px-4
                      mb-3
                      leading-tight
                      focus:outline-none focus:bg-white focus:border-gray-500
                    "
                    type="text"
                    placeholder="Prospek proyek anda"
                    v-model="campaign.description_prospek"
                  ></textarea>
                </div>
                <div class="w-full px-3">
                  <label
                    class="
                      block
                      uppercase
                      tracking-wide
                      text-gray-700 text-xs
                      font-bold
                      mb-2
                    "
                  >
                    Deskripsi Risiko
                  </label>
                  <textarea
                    rows="5"
                    class="
                      appearance-none
                      block
                      w-full
                      bg-gray-200
                      text-gray-700
                      border border-gray-200
                      rounded
                      py-3
                      px-4
                      mb-3
                      leading-tight
                      focus:outline-none focus:bg-white focus:border-gray-500
                    "
                    type="text"
                    placeholder="Risiko proyek anda"
                    v-model="campaign.description_risiko"
                  ></textarea>
                </div>
                <div class="w-full px-3">
                  <label
                    class="
                      block
                      uppercase
                      tracking-wide
                      text-gray-700 text-xs
                      font-bold
                      mb-2
                    "
                  >
                    Deskripsi Kelompok Tani
                  </label>
                  <textarea
                    rows="5"
                    class="
                      appearance-none
                      block
                      w-full
                      bg-gray-200
                      text-gray-700
                      border border-gray-200
                      rounded
                      py-3
                      px-4
                      mb-3
                      leading-tight
                      focus:outline-none focus:bg-white focus:border-gray-500
                    "
                    type="text"
                    placeholder="Deskripsikan kelompok tani"
                    v-model="campaign.description_kelompok_tani"
                  ></textarea>
                </div>
              </div>
            </form>
            <div class="block w-full text-right">
              <button
                @click="save"
                class="
                  bg-button
                  text-white
                  font-bold
                  px-4
                  py-1
                  rounded
                  inline-flex
                  items-center
                "
              >
                Simpan
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>
    <Footer />
  </div>
</template>
<script>
export default {
  middleware: "auth",

  data() {
    return {
      campaign: {
        name: "",
        short_description: "",
        description_komoditas: "",
        description_prospek: "",
        description_risiko: "",
        description_kelompok_tani: "",
        goal_amount: "",
        min_pembayaran: "",
        perks: "",
      },
    };
  },

  methods: {
    async save() {
      try {
        let response = await this.$axios.$post("/api/v1/projek", this.campaign);
        this.$router.push({
          name: "dashboard-projek-id",
          params: { id: response.data.id },
        });
        console.log(response);
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
<style lang="scss">
.v-alert {
  margin: 2rem 0;
  position: relative;
  background-color: rgba(17, 132, 255, 0.145) !important;

  .v-alert__border--top {
    top: 0;
    background-color: rgba(17, 132, 255, 0.576) !important;
  }

  .v-alert__wrapper {
    display: flex;
    gap: 1rem;

    .v-icon {
      color: rgba(17, 132, 255, 0.576);
    }
  }
}

.v-text-field {
  padding-top: 12px;
  margin-left: 0.8rem;
}

.v-text-field__details {
  display: none !important;
}

/* form */
// input:focus,
// textarea:focus {
//   background-color: yellow !important;
// }
</style>
