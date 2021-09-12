<template>
  <div class="landing-page">
    <Hero />
    <Fitur />
    <section class="container mx-auto pt-24" id="project">
      <div class="flex justify-between items-center">
        <div class="w-auto">
          <h2 class="text-xl text-gray-900 mb-8">
            Proyek Terbaru yang
            <br />
            Memerlukan Bantuan
          </h2>
        </div>
        <div class="w-auto mt-5">
          <nuxt-link
            class="text-gray-900 hover:underline text-md font-medium"
            to="/all-projek"
            >Lihat Semua</nuxt-link
          >
        </div>
      </div>
      <div class="grid grid-cols-3 mt-3 gap-y-10 gap-x-6">
        <div
          v-for="campaign in projek.data"
          :key="campaign.id"
          class="card-project border rounded-6 p-4"
        >
          <div class="item flex flex-col">
            <figure class="item-image relative">
              <img
                width="200"
                height="150"
                :src="$axios.defaults.baseURL + '/' + campaign.image_url"
                alt=""
                class="object-contain w-full h-full"
              />
            </figure>
            <div class="item-meta">
              <h4 class="text-md font-medium text-gray-900 mt-5">
                {{ campaign.name }}
              </h4>
              <p class="text-sm font-light text-gray-900 mb-4">
                {{ campaign.short_description }}
              </p>
              <!-- Progrees Bar -->
              <v-tooltip
                bottom
                v-if="campaign.goal_amount - campaign.current_amount == 0"
              >
                <template
                  class="pt-4 progress-bar"
                  v-slot:activator="{ on, attrs }"
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
                      h-3
                      rounded-lg
                    "
                    dark
                    v-bind="attrs"
                    v-on="on"
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
                        bg-green-500
                      "
                    ></div>
                  </div>
                </template>
                <span>{{
                  (campaign.current_amount / campaign.goal_amount) * 100 + "%"
                }}</span>
              </v-tooltip>
              <v-tooltip bottom v-else>
                <template
                  class="pt-4 progress-bar"
                  v-slot:activator="{ on, attrs }"
                >
                  <span
                    class="
                      overflow-hidden
                      h-2
                      mb-4
                      text-xs
                      flex
                      rounded
                      bg-gray-200
                      h-3
                      rounded-lg
                    "
                    dark
                    v-bind="attrs"
                    v-on="on"
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
                        bg-purple-progress
                      "
                    ></div>
                  </span>
                </template>
                <span>{{
                  (campaign.current_amount / campaign.goal_amount) * 100 + "%"
                }}</span>
              </v-tooltip>

              <!-- Saldo -->
              <div class="flex progress-info justify-between align-center">
                <div v-if="campaign.goal_amount - campaign.current_amount == 0">
                  <p class="ml-auto font-semibold text-green-500 text-md">
                    Terdanai Penuh
                  </p>
                </div>
                <div v-else>
                  Tersisa <br />
                  <p alt="tersisa" class="ml-auto font-semibold">
                    Rp{{
                      new Intl.NumberFormat().format(
                        campaign.goal_amount - campaign.current_amount
                      )
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
                bg-green-button
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
                bg-orange-button
                hover:bg-green-button
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
    <Story />
    <div class="cta-clip -mt-20"></div>
    <CallToAction />
    <Footer />
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
};
</script>

<style lang="scss"></style>
