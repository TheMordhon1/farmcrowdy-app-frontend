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
        <div class="w-3/4 mr-6">
          <h3 class="text-xl lg:text-2xl text-gray-900 mb-4 capitalize">
            detail proyek
          </h3>
        </div>
        <div
          class="w-1/4 text-right"
          v-if="campaign.data.goal_amount - campaign.data.current_amount == 0"
        >
          <nuxt-link
            :to="{
              name: 'dashboard-projek-id-edit',
              params: { id: campaign.data.id },
            }"
            class="
              hidden
              bg-green-button
              hover:bg-green-button
              text-white
              font-bold
              px-4
              py-1
              rounded
              inline-flex
              items-center
            "
          >
            Edit
          </nuxt-link>
        </div>
        <div class="w-1/4 text-right" v-else>
          <nuxt-link
            :to="{
              name: 'dashboard-projek-id-edit',
              params: { id: campaign.data.id },
            }"
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
            Edit
          </nuxt-link>
        </div>
      </div>
      <div class="block mb-2">
        <div class="w-full lg:max-w-full lg:flex mb-4">
          <div
            class="
              lg:border
              w-full
              lg:border-gray-400
              bg-white
              rounded
              lg:p-8
              py-5
              flex flex-col
              justify-between
              leading-normal
            "
          >
            <div>
              <div
                class="
                  text-gray-900
                  font-bold
                  text-xl
                  lg:text-2xl
                  mb-1
                  capitalize
                "
              >
                "{{ campaign.data.name }}"
              </div>
              <div class="text-gray-300 font-bold text-md mb-4 capitalize">
                {{ campaign.data.address }}
              </div>
              <p class="font-bold flex items-center capitalize text-md mb-2">
                deskripsi singkat
              </p>
              <p class="text-gray-700 text-base">
                {{ campaign.data.short_description }}
              </p>
              <!-- Deskripsi Komoditas -->
              <p
                class="font-bold flex items-center mt-3 capitalize text-md mb-2"
              >
                deskripsi komoditas
              </p>
              <p class="text-gray-700 text-base">
                {{ campaign.data.description_komoditas }}
              </p>

              <!-- Deskripsi Prospek -->
              <p
                class="font-bold flex items-center mt-3 capitalize text-md mb-2"
              >
                deskripsi prospek
              </p>
              <p class="text-gray-700 text-base">
                {{ campaign.data.description_prospek }}
              </p>

              <!-- Deskripsi Risiko -->
              <p
                class="font-bold flex items-center mt-3 capitalize text-md mb-2"
              >
                deskripsi risiko
              </p>
              <p class="text-gray-700 text-base">
                {{ campaign.data.description_risiko }}
              </p>

              <!-- Deskripsi Kelompok Tani -->
              <p
                class="font-bold flex items-center mt-3 capitalize text-md mb-2"
              >
                deskripsi Kelompok Tani
              </p>
              <p class="text-gray-700 text-base">
                {{ campaign.data.description_kelompok_tani }}
              </p>
              <div
                class="relative"
                v-if="
                  campaign.data.goal_amount - campaign.data.current_amount == 0
                "
              >
                <p
                  class="
                    font-bold
                    flex
                    items-center
                    mt-4
                    capitalize
                    text-md
                    mb-2
                  "
                >
                  yang ditawarkan kepada funder
                </p>
                <ul class="list-disc ml-5">
                  <li v-for="perk in campaign.data.perks" :key="perk">
                    {{ perk }}
                  </li>
                </ul>

                <!-- Minimal Pembiayaan -->
                <p
                  class="
                    font-bold
                    flex
                    items-center
                    mb-1
                    mt-4
                    capitalize
                    text-md
                    mb-2
                  "
                >
                  Minimal Pembiayaan
                </p>
                <p class="text-2xl lg:text-4xl text-gray-700 text-base">
                  Rp.{{
                    new Intl.NumberFormat().format(campaign.data.min_pembayaran)
                  }}
                </p>

                <!-- Total Pembiayaan -->
                <p
                  class="
                    font-bold
                    flex
                    items-center
                    mb-1
                    mt-4
                    capitalize
                    text-md
                    mb-2
                  "
                >
                  total biaya proyek
                </p>
                <p class="text-2xl lg:text-4xl text-gray-700 text-base">
                  Rp.{{
                    new Intl.NumberFormat().format(campaign.data.goal_amount)
                  }}
                </p>

                <img
                  class="
                    absolute
                    z-0
                    opacity-20
                    -top-10
                    lg:top-0 lg:right-0 lg:w-1/3 lg:z-0
                  "
                  src="/terdanai.svg"
                />
              </div>
              <div class="relative z-10" v-else>
                <p
                  class="
                    font-bold
                    flex
                    items-center
                    mt-4
                    capitalize
                    text-md
                    mb-2
                  "
                >
                  yang ditawarkan kepada funder
                </p>
                <ul class="list-disc ml-5">
                  <li v-for="perk in campaign.data.perks" :key="perk">
                    {{ perk }}
                  </li>
                </ul>

                <div class="flex flex-col lg:flex-row justify-between">
                  <!-- Minimal Pembiayaan -->
                  <div>
                    <p
                      class="
                        font-bold
                        flex
                        items-center
                        mb-1
                        mt-4
                        capitalize
                        text-md
                        mb-2
                      "
                    >
                      Minimal Pembiayaan
                    </p>
                    <p class="text-2xl lg:text-4xl text-gray-700 text-base">
                      Rp.{{
                        new Intl.NumberFormat().format(
                          campaign.data.min_pembayaran
                        )
                      }}
                    </p>
                  </div>

                  <div>
                    <!-- Total -->
                    <p
                      class="
                        font-bold
                        flex
                        items-center
                        mb-1
                        mt-4
                        capitalize
                        text-md
                        mb-2
                      "
                    >
                      total biaya proyek
                    </p>
                    <p class="text-2xl lg:text-4xl text-gray-700 text-base">
                      Rp.{{
                        new Intl.NumberFormat().format(
                          campaign.data.goal_amount
                        )
                      }}
                    </p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Gambar Proyek -->
      <div class="flex justify-between items-center">
        <div class="w-3/4 mr-6">
          <h3 class="text-xl lg:text-2xl text-gray-900 mb-4 mt-5">
            Gambar Proyek
          </h3>
        </div>
        <div class="hidden lg:block w-2/4 text-right">
          <input
            type="file"
            ref="file"
            @change="selectFile"
            class="border p-1 rounded overflow-hidden mr-2"
          />
          <button
            @click="upload"
            class="
              bg-button
              text-white
              font-bold
              px-4
              p-2
              rounded
              inline-flex
              items-center
            "
          >
            Upload
          </button>
        </div>
      </div>
      <div class="grid grid-cols-4 gap-4 -mx-2">
        <div
          class="
            relative
            w-full
            bg-white
            m-2
            p-2
            lg:border lg:border-gray-400 lg:rounded
          "
          v-for="image in campaign.data.images"
          :key="image.image_url"
        >
          <figure class="item-thumbnail-remove" @click="remove(data.images)">
            <img
              :src="$axios.defaults.baseURL + '/' + image.image_url"
              alt=""
              class="lg:rounded w-full"
            />
          </figure>
        </div>
      </div>
      <!-- Mobile input image -->
      <div class="lg:hidden block w-full text-center flex mt-5">
        <input
          type="file"
          ref="file"
          @change="selectFile"
          class="border p-1 rounded overflow-hidden mr-2"
        />
        <button
          @click="upload"
          class="
            bg-button
            text-white
            font-bold
            px-4
            p-2
            rounded
            inline-flex
            items-center
          "
        >
          Upload
        </button>
      </div>
      <!-- Mobile Input Image -->
      <div class="flex justify-between items-center">
        <div class="w-3/4 mr-6">
          <h3
            class="text-xl lg:text-2xl text-gray-900 mb-2 lg:mb-4 mt-8 lg:mt-5"
          >
            Daftar Transaksi Masuk
          </h3>
        </div>
      </div>
      <div class="block mb-2">
        <div
          class="w-full lg:max-w-full lg:flex mb-4"
          v-for="transaction in transactions.data"
          :key="transaction.id"
        >
          <div
            class="
              w-full
              lg:border-gray-400
              bg-white
              rounded
              lg:p-8
              border-b-2
              py-5
              flex flex-col
              justify-between
              leading-normal
            "
          >
            <div>
              <div class="text-gray-900 font-bold text-md mb-1">
                {{ transaction.name }}
              </div>
              <p class="text-sm text-gray-600 flex items-center mb-2">
                Rp.
                {{ new Intl.NumberFormat().format(transaction.amount) }}
                <br />{{
                  new Date(transaction.created_at)
                    | dateFormat("DD/MM/YYYY, hh:mm a")
                }}
              </p>
              <div>
                <span
                  v-if="transaction.status == 'pending'"
                  class="text-orange-button capitalize"
                >
                  {{ transaction.status }}
                </span>
                <span
                  v-else="transaction.status == 'paid'"
                  class="text-green-button capitalize"
                >
                  {{ transaction.status }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <Footer />
  </div>
</template>
<script>
import Vue from "vue";
import VueFilterDateFormat from "vue-filter-date-format";

Vue.use(VueFilterDateFormat);

export default {
  middleware: "auth",
  async asyncData({ $axios, params }) {
    const campaign = await $axios.$get("/api/v1/projek/" + params.id);
    const transactions = await $axios.$get(
      "/api/v1/projek/" + params.id + "/transaksi"
    );

    return { campaign, transactions };
  },

  data() {
    return {
      selectedFiles: undefined,
    };
  },

  methods: {
    selectFile() {
      this.selectedFiles = this.$refs.file.files;
    },
    async load() {
      const campaign = await this.$axios.$get(
        "/api/v1/projek/" + this.$route.params.id
      );
      this.campaign = campaign;
    },
    async upload(file) {
      let formData = new FormData();

      formData.append("campaign_id", this.$route.params.id);
      formData.append("file", this.selectedFiles.item(0));
      formData.append("is_primary", true);

      try {
        let response = await this.$axios.post(
          "/api/v1/projek-images",
          formData,
          {
            headers: {
              "Content-Type": "multipart/form-data",
            },
          }
        );
        console.log(response);

        this.load();
        this.selectedFiles = undefined;
      } catch (err) {
        console.log(err);
      }
    },
    remove(data) {
      const index = this.selectedFiles.indexOf(data.images);
      if (index >= 0) this.selectedFiles.splice(index, 1);
    },
  },
};
</script>
<style lang="css">
.label-terdanai-img {
  z-index: 0;
}
</style>
