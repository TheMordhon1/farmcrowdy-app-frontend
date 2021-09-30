<template>
  <div class="landing-page">
    <section class="dashboard-header pt-5">
      <div class="container mx-auto relative">
        <Navbar2 />
      </div>
    </section>
    <section class="container px-5 md:px-0 mx-auto pt-10 lg:pt-24" id="project">
      <div class="flex justify-between items-center">
        <div class="w-auto">
          <h2 class="text-xl text-gray-900 mb-8">
            Proyek Terbaru yang
            <br />
            Memerlukan Bantuan
          </h2>
        </div>
      </div>
      <ul class="flex mt-2 lg:flex-row flex-col">
        <li class="py-2 text-center lg:mr-6">
          <p class="font-bold">Semua Proyek</p>
        </li>
        <li class="py-2 text-center lg:mr-6">
          <nuxt-link
            class="text-gray-500 hover:text-gray-800"
            to="/semua-proyek/terdanai"
          >
            Terdanai
          </nuxt-link>
        </li>
        <li class="py-2 text-center lg:mr-6">
          <nuxt-link
            class="text-gray-500 hover:text-gray-800"
            to="/semua-proyek/belum-terdanai"
          >
            Belum Terdanai
          </nuxt-link>
        </li>
      </ul>
      <hr class="mt-2 mb-5" />
      <div class="grid grid-cols-1 lg:grid-cols-3 mt-3 gap-y-10 gap-x-6">
        <div
          v-for="campaign in projek.data"
          :key="campaign.id"
          class="card-project border rounded-6 p-4"
          :title="campaign.name"
        >
          <div class="item flex flex-col">
            <figure class="item-image relative">
              <img
                :src="$axios.defaults.baseURL + '/' + campaign.image_url"
                alt=""
                class="w-full img-proyek"
              />
            </figure>
            <div class="item-meta">
              <h3
                class="text-lg font-medium text-gray-900 mt-5"
                v-if="campaign.name.length < 33"
                :title="campaign.name"
              >
                {{ campaign.name }}
              </h3>
              <h3
                class="text-lg font-medium text-gray-900 mt-5"
                v-if="campaign.name.length > 33"
                :title="campaign.name"
              >
                {{ campaign.name.substring(0, 33) + "..." }}
              </h3>
              <p
                class="text-sm font-light text-gray-900 mb-4"
                v-if="campaign.short_description.length < 90"
              >
                {{ campaign.short_description }}
              </p>
              <p
                class="text-sm font-light text-gray-900 mb-4"
                v-if="campaign.short_description.length > 90"
              >
                {{ campaign.short_description.substring(0, 90) + "..." }}
              </p>
              <!-- Progrees Bar -->
              <div
                class="progress-bar"
                v-if="campaign.goal_amount - campaign.current_amount == 0"
              >
                <div
                  class="
                    overflow-hidden
                    h-2
                    mb-4
                    text-xs
                    flex
                    rounded
                    bg-gray-200
                    lg:h-3
                    h-2
                    rounded-lg
                  "
                >
                  <div
                    :style="
                      'width: ' +
                      (campaign.current_amount / campaign.goal_amount) * 100 +
                      '%'
                    "
                    class="
                      shadow-none
                      flex flex-col
                      text-center
                      whitespace-nowrap
                      text-white
                      justify-center
                      bg-green
                    "
                  ></div>
                </div>
              </div>
              <div class="progress-bar" v-else>
                <div
                  class="
                    overflow-hidden
                    h-2
                    mb-4
                    text-xs
                    flex
                    rounded
                    bg-gray-200
                    lg:h-3
                    h-2
                    rounded-lg
                  "
                >
                  <div
                    :style="
                      'width: ' +
                      (campaign.current_amount / campaign.goal_amount) * 100 +
                      '%'
                    "
                    class="
                      shadow-none
                      flex flex-col
                      text-center
                      whitespace-nowrap
                      text-white
                      justify-center
                      bg-blue
                    "
                  ></div>
                </div>
              </div>

              <!-- Saldo -->
              <div class="flex progress-info justify-between align-center">
                <div v-if="campaign.goal_amount - campaign.current_amount == 0">
                  <p class="ml-auto font-semibold color-green text-sm">
                    Terdanai <br />
                    Penuh
                  </p>
                </div>
                <div v-else-if="campaign.current_amount == 0">
                  <p class="ml-auto font-semibold color-blue text-sm">
                    Belum Ada <br />
                    Pembiayaan Masuk
                  </p>
                </div>
                <div v-else>
                  Terkumpul <br />
                  <p class="ml-auto font-semibold">
                    Rp{{
                      new Intl.NumberFormat().format(campaign.current_amount)
                    }}
                  </p>
                </div>
                <div>
                  Total <br />
                  <p alt="tersisa" class="ml-auto font-semibold">
                    Rp{{ new Intl.NumberFormat().format(campaign.goal_amount) }}
                  </p>
                </div>
              </div>
            </div>
            <button
              @click="
                $router.push({
                  name: 'projek-id',
                  params: { id: campaign.id },
                })
              "
              class="
                mt-5
                button-cta
                block
                w-full
                bg-button-green
                text-white
                font-semibold
                px-6
                py-2
                text-lg
              "
              v-if="campaign.goal_amount - campaign.current_amount == 0"
            >
              Lihat Proyek
            </button>
            <button
              @click="
                $router.push({
                  name: 'projek-id',
                  params: { id: campaign.id },
                })
              "
              class="
                mt-5
                button-cta
                block
                w-full
                bg-button
                text-white
                font-semibold
                px-6
                py-2
                text-lg
              "
              v-else
            >
              Bantu Proyek Ini
            </button>
            <p class="mt-2 text-sm">
              <span class="font-light text-gray-900 text-sm"
                >Di update pada </span
              >{{
                new Date(campaign.updated_at)
                  | dateFormat("DD-MM-YYYY, hh:mm a")
              }}
            </p>
          </div>
        </div>
      </div>
    </section>
    <Footer2 />
  </div>
</template>

<script>
import Vue from "vue";
import VueFilterDateFormat from "vue-filter-date-format";
import Story from "~/components/Story.vue";

Vue.use(VueFilterDateFormat);
export default {
  components: { Story },
  async asyncData({ $axios }) {
    const projek = await $axios.$get("/api/v1/projek");
    return { projek };
  },

  inject: {
    theme: {
      default: { isDark: false },
    },
  },
};
</script>
