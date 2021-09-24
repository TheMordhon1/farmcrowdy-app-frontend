<template lang="">
  <div class="h-screen flex justify-center items-center">
    <div
      class="
        hidden
        md:block
        lg:w-1/3
        bg-white
        h-full
        auth-background
        rounded-tr-lg rounded-br-lg
      "
    ></div>
    <div class="w-auto md:w-2/4 lg:w-2/3 flex justify-center items-center">
      <div class="w-full lg:w-1/2 px-10 lg:px-0">
        <h2 class="font-normal mb-6 text-3xl text-white">Masuk ke Akun Anda</h2>
        <div class="mb-6">
          <div class="mb-4">
            <div class="mb-4">
              <v-text-field
                v-model="login.email"
                label="Email"
                :rules="[rules.required, rules.email]"
                placeholder="ex: ardisapt@gmail.com"
                persistent-hint
                outlined
                class="form-input"
              >
              </v-text-field>
            </div>
          </div>
          <div class="mb-6">
            <div class="mb-4">
              <v-text-field
                @keyup.enter="userLogin"
                v-model="login.password"
                :append-icon="show3 ? 'mdi-eye' : 'mdi-eye-off'"
                :rules="[rules.required]"
                :type="show3 ? 'text' : 'password'"
                label="Password"
                @click:append="show3 = !show3"
                persistent-hint
                outlined
                class="form-input"
              >
              </v-text-field>
            </div>
          </div>
        </div>

        <div class="mb-6">
          <div class="mb-4">
            <button
              @click="userLogin"
              class="
                block
                w-full
                bg-button
                text-white
                font-semibold
                px-6
                py-4
                text-lg
                rounded-full
              "
            >
              Login
            </button>
          </div>
        </div>
        <div class="text-center">
          <p class="text-white text-md">
            Belum punya akun ?
            <nuxt-link to="/daftar" class="no-underline color-blue"
              >Daftar</nuxt-link
            >
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
// https://auth.nuxtjs.org/api/auth/#loginwithstrategyname-args
// Scheme link : https://auth.nuxtjs.org/schemes/local/#usage

export default {
  layout: "auth",
  data() {
    return {
      login: {
        email: "",
        password: "",
      },
      show3: false,
      rules: {
        required: (value) => !!value || "",
        email: (value) => {
          const pattern =
            /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
          return pattern.test(value) || "Masukan email yang benar";
        },
      },
    };
  },
  methods: {
    async userLogin() {
      try {
        let response = await this.$auth.loginWith("local", {
          data: this.login,
        });
        this.$auth.setUser(response.data.data);
        console.log(response);
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.auth-background {
  background-image: url("/sign-in-background.jpg");
  background-position: center;
  background-size: cover;
}

// .form-input {
//   &:hover {
//     border: none;
//   }
// }
</style>
