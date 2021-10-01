<template lang="">
  <div class="project-page">
    <section class="dashboard-header pt-5">
      <div class="container mx-auto relative">
        <Navbar2 />
      </div>
    </section>
    <section class="container px-5 md:px-0 mx-auto pt-8 lg:mt-10 mt-5">
      <div class="flex justify-between items-center mb-6">
        <div class="w-full lg:w-3/4">
          <h2 class="text-2xl lg:text-4xl text-gray-900 mb-8 font-medium">
            Dashboard
          </h2>
          <ul class="flex mt-2">
            <li class="mr-6">
              <nuxt-link
                class="text-gray-500 hover:text-gray-800"
                to="/dashboard"
              >
                Proyek Anda
              </nuxt-link>
            </li>
            <li class="mr-6">
              <p class="text-gray-800 font-bold">Riwayat Transaksi</p>
            </li>
          </ul>
        </div>
      </div>
      <hr />
      <div v-if="transaksi.data == 0">
          <EmptyStateTransaksi />
      </div>
      <div
        class="block mb-2"
        v-for="transaction in transaksi.data"
        :key="transaction.id"
        
        >
        <div class="w-full lg:max-w-full lg:flex mb-4">
          <div
            class="
              h-48
              lg:h-auto lg:w-48
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
              transaction.campaign.image_url +
              '\')'
            "
          ></div>
          <div
            class="
              w-full
              border-r border-b border-l border-gray-400
              lg:border-l-0 lg:border-t lg:border-gray-400
              bg-white
              rounded-b
              lg:rounded-b-none lg:rounded-r
              p-8
              flex flex-col
              justify-between
              leading-normal
            "
          >
            <div>
              <div class="text-gray-900 font-bold text-xl mb-1">
                {{ transaction.campaign.name }}
              </div>
              
              <p class="text-sm text-gray-600 flex items-center mb-2">
                Rp.
                {{ new Intl.NumberFormat().format(transaction.amount) }}
                <br />
                {{
                  new Date(transaction.created_at)
                    | dateFormat('DD/MM/YYYY, hh:mm a')
                }}
                <br />
                <div>
                    <div  v-if="transaction.status == 'pending'" class="flex lg:flex-row flex-col">
                      <span class="text-orange-button capitalize w-3/4"> {{ transaction.status }} </span>
                      <a target="_blank" :href="transaction.payment_url" class="
                        bg-button
                        hover:bg-green-button
                        text-white
                        font-bold
                        py-4
                        px-4
                        rounded
                        text-center
                        mt-2 lg:mt-0
                       ">Lanjutkan Pembayaran</a>
                    </div>
                    <div  v-else="transaction.status == 'paid'">
                      <span class="text-green-button capitalize"> {{ transaction.status }} </span>
                    </div>
                </div>
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
    <Footer2 />
  </div>
</template>
<script>
import Vue from 'vue'
import VueFilterDateFormat from 'vue-filter-date-format'

Vue.use(VueFilterDateFormat)
export default {
  middleware: 'auth',
  async asyncData({ $axios }) {
    
    const transaksi = await $axios.$get('/api/v1/transaksi')
    return { transaksi}
  },

}
</script>
<style lang=""></style>
