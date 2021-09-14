<template lang="">
  <div class="project-page">
    <section class="dashboard-header pt-5">
      <div class="container mx-auto relative">
        <Navbar />
      </div>
    </section>

    <section class="container mx-auto pt-8">
      <div class="flex justify-between items-center">
        <div class="w-full mr-6">
          <h2 class="text-4xl text-gray-900 mb-2 font-medium">Dashboard</h2>
        </div>
      </div>
      <div class="flex justify-between items-center">
        <div class="w-3/4 mr-6">
          <h3 class="text-2xl text-gray-900 mb-4 capitalize">detail proyek</h3>
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
      </div>
      <div class="block mb-2">
        <div class="w-full lg:max-w-full lg:flex mb-4">
          <div
            class="
              border
              w-full
              border-gray-400
              bg-white
              rounded
              p-8
              flex flex-col
              justify-between
              leading-normal
            "
          >
            <div>
              <div class="text-gray-900 font-bold text-2xl mb-4 capitalize">
                "{{ campaign.data.name }}"
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
                <p class="text-4xl text-gray-700 text-base">
                  Rp.{{
                    new Intl.NumberFormat().format(campaign.data.goal_amount)
                  }}
                </p>

                <img
                  class="absolute top-0 right-0 w-1/3 z-0"
                  src="/terdanai.svg"
                />
              </div>
              <div class="relative" v-else>
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
                <p class="text-4xl text-gray-700 text-base">
                  Rp.{{
                    new Intl.NumberFormat().format(campaign.data.goal_amount)
                  }}
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="flex justify-between items-center">
        <div class="w-3/4 mr-6">
          <h3 class="text-2xl text-gray-900 mb-4 mt-5">Gambar Proyek</h3>
        </div>
        <div class="w-2/4 text-right">
          <input
            type="file"
            ref="file"
            @change="selectFile"
            class="border p-1 rounded overflow-hidden mr-2"
          />
          <button
            @click="upload"
            class="
              bg-green-button
              hover:bg-green-button
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
            border border-gray-400
            rounded
          "
          v-for="image in campaign.data.images"
          :key="image.image_url"
        >
          <figure class="item-thumbnail-remove" @click="remove(data.images)">
            <img
              :src="$axios.defaults.baseURL + '/' + image.image_url"
              alt=""
              class="rounded w-full"
            />
          </figure>
        </div>
      </div>
      <div class="flex justify-between items-center">
        <div class="w-3/4 mr-6">
          <h3 class="text-2xl text-gray-900 mb-4 mt-5">
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
              border border-gray-400
              lg:border-gray-400
              bg-white
              rounded
              p-8
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
    <div class="cta-clip -mt-20"></div>
    <CallToAction />
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
<style lang=""></style>
