<template lang="">
  <header class="flex items-center fixed">
    <div style="height: 54px" class="pr-5">
      <v-avatar color="orange" size="62" class="mr-4">
        <img src="/logo@2x.png" alt="logo" class="h-full" />
      </v-avatar>
    </div>
    <ul class="flex items-center gap-10">
      <li>
        <nuxt-link class="text-white link-hover text-lg" to="/">Home</nuxt-link>
      </li>
      <li>
        <nuxt-link class="text-white link-hover text-lg" to="/#proyek"
          >Proyek</nuxt-link
        >
      </li>
      <li>
        <nuxt-link class="text-white link-hover text-lg" to="/#fitur"
          >Fitur</nuxt-link
        >
      </li>
      <li>
        <nuxt-link class="text-white link-hover text-lg" to="/#story"
          >Kisah Sukses</nuxt-link
        >
      </li>
    </ul>
    <ul
      class="flex justify-between ml-auto"
      v-if="!this.$store.state.auth.loggedIn"
    >
      <li>
        <nuxt-link
          to="/daftar"
          class="
            inline-block
            bg-transparent
            border-white border
            hover:bg-white hover:bg-opacity-25
            text-white
            font-light
            w-40
            text-center
            px-6
            py-1
            text-lg
            rounded-full
            mr-4
          "
        >
          Daftar
        </nuxt-link>
      </li>
      <li>
        <nuxt-link
          to="/login"
          class="
            inline-block
            bg-transparent
            border-white border
            hover:bg-white hover:bg-opacity-25
            text-white
            font-light
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
    </ul>
    <div class="ml-auto" v-else>
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
                $axios.defaults.baseURL + '/' + $store.state.auth.user.image_url
              "
              alt=""
            />
          </v-avatar>
          <span class="mr-1 capitalize">
            {{ this.$store.state.auth.user.name }}
          </span>
          <!-- <img
            src="https://lh3.googleusercontent.com/ogw/ADea4I4IqCnUbvNZ0GCf2OGklYSIYMDsfW4xfGdWMaGobQ=s64-c-mo"
            alt=""
            class="h-8 rounded-full mr-2"
          />
          <span class="mr-1"> Romdon </span> -->
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
  </header>
</template>

<style scoped>
.dropdown:hover .dropdown-menu {
  display: block;
}
</style>

<script>
export default {
  methods: {
    async logout() {
      await this.$auth.logout();
    },
  },
};
</script>
