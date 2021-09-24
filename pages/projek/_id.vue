<template>
  <div class="project-page">
    <section class="project-header pt-5">
      <div class="container mx-auto relative">
        <Navbar />
      </div>
    </section>
    <section class="container project-container mx-auto -mt-56">
      <div class="flex mt-3">
        <div style="width: 72%" class="mr-6">
          <div class="bg-white p-3 mb-3 border border-gray-400 rounded-20">
            <figure class="item-image">
              <img :src="default_image" alt="" class="rounded-20 w-full h-66" />
            </figure>
          </div>
          <div class="flex -mx-2">
            <div
              v-for="image in campaign.data.images"
              :key="image.image_url"
              class="
                relative
                w-1/4
                bg-white
                m-2
                p-2
                border border-gray-400
                rounded-20
              "
            >
              <figure class="item-thumbnail cursor-pointer">
                <img
                  :src="$axios.defaults.baseURL + '/' + image.image_url"
                  @click="
                    changeImage($axios.defaults.baseURL + '/' + image.image_url)
                  "
                  alt=""
                  class="rounded-20 w-full"
                />
              </figure>
            </div>
          </div>
        </div>
        <div style="width: 28%">
          <div
            class="bg-white w-full p-5 border border-gray-400 rounded-20 sticky"
            style="top: 15px"
          >
            <h3 class="font-semibold">Pembuat proyek :</h3>

            <div class="flex mt-3">
              <div>
                <img
                  :src="
                    $axios.defaults.baseURL + '/' + campaign.data.user.image_url
                  "
                  alt=""
                  class="w-16 inline-block rounded-full h-16"
                />
              </div>
              <div class="w-3/4 ml-5 mt-1">
                <div class="font-semibold text-xl text-gray-800">
                  {{ campaign.data.user.name }}
                </div>
                <div class="text-sm text-gray-800 capitalize">
                  ({{ campaign.data.user.occupation }})
                </div>

                <div class="font-light text-md text-gray-400 mt-2">
                  {{ campaign.data.backer_count }} Funder
                </div>
              </div>
            </div>

            <!-- Status -->
            <h3 class="flex mt-5 font-semibold gap-2">
              Status proyek :
              <p
                v-if="
                  campaign.data.goal_amount - campaign.data.current_amount == 0
                "
                class="color-green"
              >
                Terdanai
              </p>

              <div v-else class="status flex gap-3">
                <p class="color-blue relative">Berjalan</p>
                <v-app>
                  <v-tooltip top class="absolute p-5">
                    <template v-slot:activator="{ on, attrs }">
                      <v-btn color="primary" dark v-bind="attrs" v-on="on">
                        ?
                      </v-btn>
                    </template>
                    <span
                      >Dana disalurkan jika sudah mencapai Rp{{
                        new Intl.NumberFormat().format(
                          campaign.data.goal_amount * 0.75
                        )
                      }}
                    </span>
                  </v-tooltip>
                </v-app>
              </div>
            </h3>

            <!-- Perks -->
            <h4 class="mt-5 font-semibold">Yang akan didapatkan :</h4>
            <ul class="list-check mt-3">
              <li v-for="perk in campaign.data.perks" :key="perk">
                {{ perk }}
              </li>
            </ul>

            <!-- Min Pembayaran -->
            <div class="flex mt-5 justify-between">
              <div>
                <h3 class="font-regular text-sm">Min.Pembiayaan</h3>
                <p class="font-semibold">
                  Rp
                  {{
                    new Intl.NumberFormat().format(campaign.data.min_pembayaran)
                  }}
                </p>
              </div>

              <div>
                <h3 class="font-regular text-sm">Maks.Pembiayaan</h3>
                <p class="font-semibold">
                  Rp
                  {{
                    new Intl.NumberFormat().format(
                      campaign.data.goal_amount - campaign.data.current_amount
                    )
                  }}
                </p>
              </div>
            </div>

            <!-- Input Nominal -->
            <div
              v-if="
                campaign.data.goal_amount - campaign.data.current_amount == 0
              "
            >
              <div class="hidden">
                <template v-if="this.$store.state.auth.loggedIn">
                  <input
                    class="
                      border border-gray-500
                      block
                      w-full
                      px-6
                      py-3
                      mt-4
                      rounded-full
                      text-gray-800
                      transition
                      duration-300
                      ease-in-out
                      focus:outline-none focus:shadow-outline
                    "
                    type="number"
                    placeholder="Jumlah Dalam Rp"
                    v-model.number="transactions.amount"
                    @keyup.enter="fund"
                  />
                  <button
                    @click="fund"
                    class="
                      mt-3
                      block
                      w-full
                      bg-button
                      text-white
                      font-medium
                      px-6
                      py-3
                      text-md
                      rounded-full
                    "
                  >
                    Bantu Sekarang
                  </button>
                </template>
                <template v-else>
                  <button
                    @click="$router.push({ path: '/login' })"
                    class="
                      mt-3
                      button-cta
                      block
                      w-full
                      bg-button
                      text-white
                      font-medium
                      px-6
                      py-3
                      text-md
                      rounded-full
                    "
                  >
                    Bantu Sekarang
                  </button>
                </template>
              </div>
            </div>
            <div v-else>
              <div class="block">
                <template v-if="this.$store.state.auth.loggedIn">
                  <input
                    class="input-rp"
                    required
                    type="number"
                    placeholder="Nominal Dalam Rp"
                    v-model.number="transactions.amount"
                    @keyup.enter="fund"
                    :step="campaign.data.min_pembayaran"
                    :max="
                      campaign.data.goal_amount - campaign.data.current_amount
                    "
                    :min="campaign.data.min_pembayaran"
                  />

                  <button
                    @click="fund"
                    class="
                      mt-3
                      button-cta
                      block
                      w-full
                      bg-button
                      hover:bg-green-button
                      text-white
                      font-medium
                      px-6
                      py-3
                      text-md
                      rounded-full
                      text-center
                    "
                  >
                    Bantu Sekarang
                  </button>
                </template>
                <template v-else>
                  <a
                    target="_blank"
                    @click="$router.push({ path: '/login' })"
                    class="
                      mt-5
                      button-cta
                      block
                      w-full
                      bg-button-rounded
                      text-white
                      font-medium
                      px-6
                      py-3
                      text-md
                      rounded-full
                      text-center
                      cursor-pointer
                    "
                  >
                    Login Dulu
                  </a>
                </template>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <template v>
      <div class="container mx-auto pt-8">
        <div class="flex justify-between items-center">
          <div class="w-full md:w-3/4 mr-6">
            <h2 class="text-4xl text-gray-900 mb-1 font-medium">
              {{ campaign.data.name }}
            </h2>
            <p class="text-md text-gray-300 mb-2 font-medium">
              {{ campaign.data.address }}
            </p>
            <p class="font-light text-xl mb-5">
              {{ campaign.data.short_description }}
            </p>

            <div
              class="relative progress-bar"
              v-if="
                campaign.data.goal_amount - campaign.data.current_amount == 0
              "
            >
              <div
                class="
                  overflow-hidden
                  mb-4
                  text-xs
                  flex
                  rounded-full
                  bg-gray-200
                  h-6
                "
              >
                <div
                  :style="
                    'width: ' +
                    (campaign.data.current_amount / campaign.data.goal_amount) *
                      100 +
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
            <div class="relative progress-bar" v-else>
              <div
                class="
                  overflow-hidden
                  mb-4
                  text-xs
                  flex
                  rounded-full
                  bg-gray-200
                  h-6
                "
              >
                <div
                  :style="
                    'width: ' +
                    (campaign.data.current_amount / campaign.data.goal_amount) *
                      100 +
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
            <div class="flex progress-info justify-between align-center mb-10">
              <div
                v-if="
                  campaign.data.goal_amount - campaign.data.current_amount == 0
                "
              >
                <p class="ml-auto font-semibold text-xl color-green">
                  Terdanai Penuh
                </p>
              </div>
              <div v-else>
                Terkumpul <br />
                <p class="ml-auto font-semibold text-xl flex relative">
                  Rp{{
                    new Intl.NumberFormat().format(campaign.data.current_amount)
                  }}
                </p>
              </div>
              <div>
                Total <br />
                <p class="ml-auto font-semibold text-xl">
                  Rp{{
                    new Intl.NumberFormat().format(campaign.data.goal_amount)
                  }}
                </p>
              </div>
            </div>

            <span class="capitalize font-semibold text-2xl mb-3"
              >tentang komoditas</span
            >
            <p class="font-light text-xl mb-5 mb-10">
              {{ campaign.data.description_komoditas }}
            </p>

            <span class="capitalize font-semibold text-2xl mb-3">Prospek</span>
            <p class="font-light text-xl mb-5 mb-10">
              {{ campaign.data.description_prospek }}
            </p>

            <span class="capitalize font-semibold text-2xl mb-3">Risiko</span>
            <p class="font-light text-xl mb-5 mb-10">
              {{ campaign.data.description_risiko }}
            </p>

            <span class="capitalize font-semibold text-2xl mb-3"
              >kelompok tani</span
            >
            <p class="font-light text-xl mb-5 mb-10">
              {{ campaign.data.description_kelompok_tani }}
            </p>
          </div>
          <div class="w-1/4 hidden md:block"></div>
        </div>
      </div>
    </template>
    <Footer />
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, params }) {
    const campaign = await $axios.$get("/api/v1/projek/" + params.id);
    return { campaign };
  },
  data: function () {
    return {
      default_image: "",
      transactions: {
        amount: "",
        campaign_id: Number.parseInt(this.$route.params.id),
      },
      number: "",
    };
  },

  watch: {
    number() {
      this.number = this.number.replace(/[^0-9]/g, "");
    },
  },

  methods: {
    async fund() {
      try {
        let response = await this.$axios.$post(
          "/api/v1/transaksi",
          this.transactions
        );
        window.location = response.data.payment_url;
        console.log(response.data.payment_url);
      } catch (error) {
        console.log(error);
      }
    },
    changeImage(url) {
      this.default_image = url;
    },
  },
  mounted() {
    this.default_image =
      this.$axios.defaults.baseURL + "/" + this.campaign.data.image_url;
  },
};
</script>

<style lang="scss">
.v-tooltip__content {
  background: rgb(9, 8, 8) !important;
  font-size: 12px !important;
  line-height: 15px !important;
  padding: 5px 10px !important;
  left: 0 !important;
  position: absolute !important;
}
/* Input Nominal */

.input-rp {
  border: 1px solid #333;
  border-radius: 30px;
  background: #f1f1f1;
  padding: 1rem;
  width: 100%;
  margin-top: 1rem;
  color: #555;
  transition: 0.5s ease-in-out;
}
</style>
