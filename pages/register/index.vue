<template>
  <div class="bg d-flex">
    <div class="row">
      <div class="left col-md-6">
        <div class="container mt-5 text-white">
          <h3>Sign Up</h3>
          <div class="mt-3">
            <p>A world class education for anyone, anywhere. 100% free.</p>
            <p>
              Join Fullstack Academy to get personalized help with what you’re
              studying or to learn something completely new. We’ll save all of
              your progress.
            </p>
            <p>
              By signing up for Fullstack Academy, you agree to our Terms of use
              and Privacy Policy.
            </p>
          </div>
        </div>
      </div>
      <div class="col-md-6">
        <div class="container mt-5">
          <!-- <p>Join Fullstack Academy as a</p>
          <div class="btn-group btn-group-toggle" data-toggle="buttons">
            <label class="btn btn-primary active">
              <input
                type="radio"
                name="user"
                id="option1"
                autocomplete="off"
                checked
              />
              Student
            </label>
            <label class="btn btn-primary">
              <input
                type="radio"
                name="admin"
                id="option2"
                autocomplete="off"
              />
              Tutor
            </label>
          </div> -->
          <form @submit.prevent="submitForm">
            <div class="mt-3">
              <div class="form-group">
                <label for="email">Email</label>
                <input
                  id="email"
                  type="email"
                  :class="
                    invalid
                      ? `form-control is-invalid mb-2`
                      : 'form-control mb-2'
                  "
                  placeholder="Your email address"
                  v-model="email"
                  required
                />

                <div class="invalid-feedback">
                  Format email salah.
                </div>
              </div>
              <div class="form-group">
                <label for="name">Name</label>
                <input
                  id="name"
                  type="text"
                  :class="invalid ? `form-control is-invalid` : 'form-control'"
                  placeholder="Your name"
                  v-model="nama"
                  required
                />
                <div class="invalid-feedback">
                  Nama wajib diisi
                </div>
              </div>
              <div class="form-group">
                <label for="createPassword">Password</label>
                <input
                  id="createPassword"
                  type="password"
                  :class="invalid ? `form-control is-invalid` : 'form-control'"
                  placeholder="Your password"
                  v-model="password"
                  required
                />
                <div class="invalid-feedback">
                  Password wajib diisi
                </div>
                <small id="passwordHelpBlock" class="form-text text-muted">
                  Your password must be 8-20 characters long, contain letters
                  and numbers.
                </small>
              </div>
              <div class="form-group">
                <label for="createConfirmPassword">Confirm password</label>
                <input
                  id="createConfirmPassword"
                  type="password"
                  class="form-control"
                  placeholder="Confirm password"
                  v-model="passwordConfirm"
                  required
                />
                <small
                  id="passwordHelpBlock"
                  class="form-text text-muted red-text"
                  v-if="passConfirm"
                >
                  Password tidak cocok, periksa ulang kembali password anda
                </small>
              </div>
            </div>
            <div class="bottom mb-2">
              <div class="float-left mt-3 pl-3 ">
                <nuxt-link to="/login">Back</nuxt-link>
              </div>
              <div class="float-right pr-2">
                <button class="submit btn btn-primary">
                  Sign Up
                </button>
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
      email: "",
      nama: "",
      password: "",
      passwordConfirm: "",
      status: "user",
      passConfirm: false,
      invalid: false
    };
  },
  // TRIGGER INVALID BELUM//
  methods: {
    async submitForm() {
      try {
        let payload = {
          email: this.email,
          nama: this.nama,
          password: this.password,
          passwordConfirm: this.passwordConfirm,
          status: this.status
        };

        if (payload.password !== payload.passwordConfirm) {
          this.passConfirm = true;
        } else {
          const response = await this.$axios.post("/register", payload);
          console.log(response);
          this.$swal({
            icon: "success",
            title: "Registrasi Berhasil",
            timer: 3000
          });
          this.$router.push("/login");
        }
      } catch (error) {
        console.log(error);
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

.bottom {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
}
.red-text {
  color: red !important;
}
</style>
