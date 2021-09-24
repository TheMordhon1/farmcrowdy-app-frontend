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
        <h2 class="font-normal mb-6 text-3xl text-white"><i></i> Buat Akun</h2>
        <div class="mb-4">
          <div class="mb-4">
            <v-text-field
              v-model="register.name"
              label="Nama Lengkap"
              persistent-hint
              outlined
              maxlenght="20"
              counter
            ></v-text-field>
          </div>
        </div>
        <div class="mb-4">
          <div class="mb-4">
            <v-text-field
              v-model="register.occupation"
              label="Pekerjaan"
              hint="ex:Pengusaha/Petani"
              persistent-hint
              outlined
            ></v-text-field>
          </div>
        </div>
        <div class="mb-4">
          <div class="mb-4">
            <v-text-field
              v-model="register.email"
              label="Email"
              :rules="[rules.required, rules.email]"
              placeholder="ex: ardisapt@gmail.com"
              persistent-hint
              outlined
            >
            </v-text-field>
          </div>
        </div>
        <div class="mb-6">
          <div class="mb-4">
            <v-text-field
              @keyup.enter="userRegister"
              v-model="register.password"
              :append-icon="show3 ? 'mdi-eye' : 'mdi-eye-off'"
              :rules="[rules.required, rules.min, rules.inputPass]"
              :type="show3 ? 'text' : 'password'"
              label="Password"
              @click:append="show3 = !show3"
              persistent-hint
              outlined
            >
            </v-text-field>
          </div>
        </div>
        <div class="mb-4">
          <div class="mb-4">
            <button
              @click="userRegister"
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
              Lanjutkan
            </button>
          </div>
        </div>
        <div class="text-center">
          <p class="text-white text-md">
            Sudah punya akun?
            <nuxt-link to="/login" class="no-underline color-blue"
              >Log In</nuxt-link
            >
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  layout: "auth",
  data() {
    return {
      register: {
        name: "",
        email: "",
        occupation: "",
        password: "",
      },
      show3: false,
      rules: {
        required: (value) => !!value || "",
        counter: (value) => value.length <= 20 || "Max 20 Karakter",
        inputPass: (v) => v.length < 8 || "Password, OK !",
        min: (v) => v.length >= 8 || "Min 8 Karakter",
        email: (value) => {
          const pattern =
            /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
          return pattern.test(value) || "Masukan email yang benar";
        },
      },
    };
  },
  methods: {
    async userRegister() {
      try {
        let response = await this.$axios.post("/api/v1/users", this.register);
        let isEmailEvailable = await this.$axios.post(
          "/api/v1/email_checkers",
          this.register
        );
        console.log(response.data.data.token, isEmailEvailable);
        this.$auth
          .setUserToken(response.data.data.token)
          .then(() => this.$router.push({ path: "/upload" }));
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
<style scoped>
.auth-background {
  background-image: url("/sign-up-background.jpg");
  background-position: center;
  background-size: cover;
}
</style>
