<template lang="">
  <div class="font-sans antialiased" id="app">
    <nav
      class="px-5 flex items-center justify-between flex-wrap bg-nav p-2 fixed"
    >
      <div class="flex items-center flex-no-shrink text-white mr-6">
        <v-avatar class="mr-4">
          <img src="/logo@2x.png" alt="logo" class="h-30" />
        </v-avatar>
      </div>
      <div class="block sm:hidden">
        <button
          @click="toggle"
          class="
            flex
            items-center
            border
            rounded
            text-teal-lighter
            border-teal-light
            hover:border-white
            ml-auto
          "
        >
          <svg
            class="fill-current h-8 w-8"
            viewBox="0 0 20 20"
            xmlns="http://www.w3.org/2000/svg"
          >
            <title>Menu</title>
            <path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z" />
          </svg>
        </button>
      </div>
      <div
        :class="open ? 'block' : 'hidden'"
        class="
          w-full
          flex-grow
          sm:flex sm:items-center sm:w-auto
          bg-white
          lg:bg-none
          nav-mobile
          py-10
          px-5
          lg:py-0 lg:px-0 lg:-mt-2
        "
      >
        <ul
          class="
            flex flex-col
            gap-4
            lg:flex-row lg:items-center lg:gap-10
            mb-10
            lg:mb-0
          "
        >
          <li>
            <nuxt-link class="text-nav link-nav text-lg" to="/">Home</nuxt-link>
          </li>
          <li>
            <nuxt-link class="text-nav link-nav text-lg" to="/#proyek"
              >Proyek</nuxt-link
            >
          </li>
          <li>
            <nuxt-link class="text-nav link-nav text-lg" to="/#fitur"
              >Fitur</nuxt-link
            >
          </li>
          <li>
            <nuxt-link class="text-nav link-nav text-lg" to="/#story"
              >Kisah Sukses</nuxt-link
            >
          </li>
        </ul>
        <ul
          class="flex mt-2 lg:gap-4 gap-6 ml-auto mr-5"
          v-if="!this.$store.state.auth.loggedIn"
        >
          <li>
            <nuxt-link
              to="/login"
              class="
                inline-block
                bg-button-rounded-2
                hover:bg-opacity-25
                font-light
                color-blue
                w-40
                text-center
                px-6
                py-1
                text-lg
                rounded-full
              "
            >
              Masuk
            </nuxt-link>
          </li>
          <li>
            <nuxt-link
              to="/daftar"
              class="
                inline-block
                bg-button-rounded
                hover:bg-white hover:bg-opacity-25
                font-light
                w-40
                text-center text-white
                hover:color-blue
                px-6
                py-1
                text-lg
                rounded-full
              "
            >
              Daftar
            </nuxt-link>
          </li>
        </ul>
        <div class="ml-auto mr-5" v-else>
          <div class="dropdown inline-block relative z-10">
            <button
              class="
                bg-white
                text-gray-700
                font-semibold
                py-2
                px-2
                rounded
                inline-flex
                items-center
              "
            >
              <v-avatar color="orange" size="48" class="mr-4">
                <img
                  v-if="$store.state.auth.user.image_url"
                  :src="
                    $axios.defaults.baseURL +
                    '/' +
                    $store.state.auth.user.image_url
                  "
                  alt=""
                />
              </v-avatar>
              <span class="mr-1 capitalize">
                {{ this.$store.state.auth.user.name }}
              </span>

              <svg
                class="fill-current h-4 w-4"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
              >
                <path
                  d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
                />
              </svg>
            </button>
            <ul
              class="
                dropdown-menu
                absolute
                hidden
                text-gray-700
                pt-1
                shadow
                w-full
                -mt-2
              "
            >
              <li class="">
                <nuxt-link
                  class="
                    bg-white
                    hover:bg-gray-100
                    py-2
                    px-4
                    block
                    whitespace-no-wrap
                  "
                  to="/dashboard"
                  >Dashboard</nuxt-link
                >
              </li>
              <li class="">
                <nuxt-link
                  class="
                    bg-white
                    hover:bg-gray-100
                    py-2
                    px-4
                    block
                    whitespace-no-wrap
                  "
                  to="/ubah-foto"
                  >Ubah Foto</nuxt-link
                >
              </li>

              <li class="">
                <a
                  class="
                    cursor-pointer
                    rounded-b
                    bg-white
                    hover:bg-gray-100
                    border-t
                    py-2
                    px-4
                    block
                    whitespace-no-wrap
                  "
                  @click="logout()"
                  >Keluar</a
                >
              </li>
            </ul>
          </div>
        </div>
      </div>
    </nav>
  </div>
</template>

<style scoped>
.dropdown:hover .dropdown-menu {
  display: block;
}

.bg-nav {
  background: #fff;
  width: 100%;
  top: 0;
  left: 0;
  height: 64px;
  z-index: 10000;
  box-shadow: rgb(0 0 0 / 7%) 0px 4px 6px -1px;
  transition: transform 280ms ease 0s;
}

.text-nav {
  color: #a7a7a7;
  font-weight: bold;
}

.text-nav:hover {
  color: #1190cc;
}

.link-nav {
  display: block;
}

@media (max-width: 600px) {
  .nav-mobile {
    position: absolute;
    top: 64px;
    left: 0;
    box-shadow: rgb(0 0 0 / 20%) 0px 4px 6px -1px;
    transition: transform 280ms ease 0s;
  }
}
</style>

<script>
export default {
  data() {
    return {
      open: false,
    };
  },
  methods: {
    async logout() {
      await this.$auth.logout();
    },
    toggle() {
      this.open = !this.open;
    },
  },
};
</script>
