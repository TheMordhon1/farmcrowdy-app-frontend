<template lang="">
  <div class="project-page">
    <section class="dashboard-header pt-5">
      <div class="container mx-auto relative">
        <Navbar2 />
      </div>
    </section>
    <section class="container px-5 md:px-0 mx-auto pt-8 lg:mt-10 mt-5">
      <div class="flex lg:justify-between items-center mb-6">
        <div class="w-full lg:w-3/4 mr-6">
          <h2 class="text-2xl lg:text-4xl text-gray-900 mb-8 font-medium">
            Dashboard
          </h2>
          <ul class="flex mt-2">
            <li class="mr-6">
              <p class="text-gray-800 font-bold">Proyek Anda</p>
            </li>
            <li class="mr-6">
              <nuxt-link
                class="text-gray-500 hover:text-gray-800"
                to="/dashboard/transaksi"
              >
                Riwayat Transaksi
              </nuxt-link>
            </li>
          </ul>
        </div>
        <div class="w-1/4 text-right hidden" v-if="projek.data == 0">
          <nuxt-link
            to="/dashboard/projek/create"
            class="
              bg-button
              text-white
              font-bold
              py-4
              px-4
              rounded
              inline-flex
              items-center
            "
          >
            Buat Proyek</nuxt-link
          >
        </div>

        <div
          class="text-right block fixed lg:bottom-5 bottom-3 right-3 z-50"
          v-else
        >
          <nuxt-link
            to="/dashboard/projek/create"
            class="
              bg-button
              text-white
              font-bold
              py-4
              px-4
              rounded
              inline-flex
              items-center
            "
          >
            Buat Proyek</nuxt-link
          >
        </div>
      </div>
      <hr />

      <div class="block mb-2">
        <div v-if="projek.data == 0">
          <EmptyState />
        </div>
        <div
          class="w-full lg:max-w-full lg:flex mb-4"
          v-for="campaign in projek.data"
          :key="campaign.id"
        >
          <div
            class="
              border
              h-48
              lg:h-auto lg:w-64
              flex-none
              bg-cover
              rounded-t
              lg:rounded-t-none lg:rounded-l
              text-center
              overflow-hidden
            "
            :style="
              'background-color: #bbb; background-position: center; background-image: url(\'' +
              $axios.defaults.baseURL +
              '/' +
              campaign.image_url +
              '\')'
            "
          ></div>
          <nuxt-link
            :to="'/dashboard/projek/' + campaign.id"
            class="
              w-full
              border-r border-b border-l border-gray-400
              lg:border-l-0 lg:border-t lg:border-gray-400
              bg-white
              rounded-b
              lg:rounded-b-none lg:rounded-r lg:p-8
              p-4
              flex flex-col
              justify-between
              leading-normal
            "
          >
            <div class="mb-8">
              <div class="text-gray-900 font-bold text-xl mb-1">
                {{ campaign.name }}
              </div>
              <p
                class="text-sm text-gray-600 flex items-center mb-2 color-green"
                v-if="campaign.goal_amount - campaign.current_amount == 0"
              >
                Terdanai Penuh
              </p>
              <p
                class="text-sm text-gray-600 flex items-center mb-2 color-blue"
                v-else-if="campaign.current_amount == 0"
              >
                Belum Ada Pembiayaan Masuk
              </p>
              <p class="text-sm text-gray-600 flex items-center mb-2" v-else>
                Tersisa Rp.{{
                  new Intl.NumberFormat().format(
                    campaign.goal_amount - campaign.current_amount
                  )
                }}
                dari Rp.
                {{ new Intl.NumberFormat().format(campaign.goal_amount) }}
              </p>
              <p class="text-gray-700 text-base">
                {{ campaign.short_description }}
              </p>
            </div>
            <div class="flex items-center">
              <nuxt-link
                :to="'/dashboard/projek/' + campaign.id"
                class="bg-button-green text-white py-2 px-4 rounded"
              >
                Detail
              </nuxt-link>
            </div>
            <p
              class="
                text-sm text-gray-600
                flex
                items-center
                ml-auto
                mt-4
                lg:mt-0
              "
            >
              {{
                new Date(campaign.updated_at)
                  | dateFormat("DD/MM/YYYY, hh:mm a")
              }}
            </p>
          </nuxt-link>
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
  async asyncData({ $axios, app }) {
    const projek = await $axios.$get(
      "/api/v1/projek?user_id=" + app.$auth.user.id
    );
    return { projek };
  },
};
</script>
<style lang=""></style>
