<template>
  <div class="bg d-flex">
    <div class="row">
      <div class="left col-md-6">
        <div class="container mt-5 text-white">
          <h3>Login</h3>
          <p class="mt-3">
            By logging into Fullstack Academy, you agree to our Terms of use and
            Privacy Policy.
          </p>
        </div>
      </div>
      <div class="col-md-6">
        <div class="container mt-5">
          <form @submit.prevent="submitLogin">
            <div class="form-group">
              <small
                id="incorrect"
                class="form-text text-muted red-text mb-3"
                v-if="!incorrect"
              >
                Your email or password is incorrect.
              </small>
              <label for="email">Email</label>
              <input
                id="email"
                type="email"
                class="form-control mb-2"
                placeholder="Masukkan email anda"
                v-model="login.email"
                required
              />
            </div>
            <div class="form-group">
              <label for="password">Password</label>
              <div class="input-group">
                <input
                  id="password"
                  :type="showPassword ? 'password' : 'text'"
                  class="form-control"
                  placeholder="Masukkan password"
                  v-model="login.password"
                  required
                />
                <div class="input-group-append eye">
                  <span class="input-group-text bg-white"
                    ><i
                      :class="showPassword ? 'fas fa-eye-slash' : 'fas fa-eye'"
                      @click="showPassword = !showPassword"
                    ></i
                  ></span>
                </div>
              </div>
            </div>

            <div class="mt-4 ">
              <!-- <a href="/belom">
                Forgot password?
              </a> -->
              <button
                type="submit"
                class="submit btn btn-primary btn-block"
                style="margin-top:5px"
              >
                Log in
              </button>
              <div class="text-center mt-3">
                <nuxt-link to="/register" class="text-center"
                  >Create an account</nuxt-link
                >
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  layout: "login",
  auth: false,
  data() {
    return {
      login: {
        email: "",
        password: ""
      },
      showPassword: true,
      incorrect: true
    };
  },
  methods: {
    async submitLogin() {
      try {
        let response = await this.$auth.loginWith("local", {
          data: this.login
        });
        console.log(response);
        if (this.$auth.user) {
          this.$swal({
            icon: "success",
            title: `Hi, Selamat Datang ${this.$auth.user.nama}`,
            text: "Kamu berhasil login",
            timer: 3000
          });
          this.$router.push("/");
        } else {
          this.incorrect = false;
        }
      } catch (err) {
        console.log(err);
      }
    }
  }
};
</script>

<style scoped>
.bg {
  height: 100vh;
}
.row {
  background-color: rgb(255, 255, 255);
  max-width: 800px;
  height: 100vh;
  margin: auto;
  height: 70vh;
}

.left {
  background-color: #6750c0;
  background-image: linear-gradient(316deg, #7059c9 0%, #7b47b3 74%);
}
.red-text {
  color: red !important;
}
.bg-white {
  background-color: white;
}
</style>
