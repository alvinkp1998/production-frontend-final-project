<template>
  <div>
    <div class="container">
      <div class="jumbotron jumbotron-fluid">
        <div class="container profile">
          <div class="row ">
            <div class="col-md-2">
              <img
                :src="
                  user.foto ||
                    'https://w7.pngwing.com/pngs/81/570/png-transparent-profile-logo-computer-icons-user-user-blue-heroes-logo-thumbnail.png'
                "
                class="rounded-circle"
                width="180px"
                height="180px"
                data-toggle="modal"
                data-target="#exampleModal"
              />
              <div
                class="modal fade"
                id="exampleModal"
                tabindex="-1"
                aria-labelledby="exampleModalLabel"
                aria-hidden="true"
              >
                <div class="modal-dialog modal-dialog-centered">
                  <div class="modal-content">
                    <div class="modal-header">
                      <button
                        type="button"
                        class="close"
                        data-dismiss="modal"
                        aria-label="Close"
                      >
                        <span aria-hidden="true">&times;</span>
                      </button>
                    </div>
                    <div class="modal-body">
                      <div class="text-center">
                        <img
                          :src="
                            user.foto ||
                              'https://w7.pngwing.com/pngs/81/570/png-transparent-profile-logo-computer-icons-user-user-blue-heroes-logo-thumbnail.png'
                          "
                          class="rounded-circle mb-3"
                          width="250px"
                          height="250px"
                        />
                        <h3>Profile Picture</h3>
                      </div>
                    </div>
                    <div class="modal-footer">
                      <input
                        type="file"
                        class="form-control-file"
                        @change="onFileSelected"
                      />
                      <button
                        type="submit"
                        class="btn btn-primary btn-block"
                        @click="upload"
                      >
                        Ganti Foto
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="col-md-3">
              <span class="text-white ml-3 mt-4 ">{{ user.nama }}</span>
              <span class="text-white-2 ml-3 mt-5 pt-2"
                >{{ user.pekerjaan }} at {{ user.institusi }}</span
              >
            </div>
            <div class="col-md-4">
              <div class="mt-5 ml-5 pl-5">
                <p class="text-white-2">
                  <i class="fas fa-phone-square-alt"></i>
                  <span>{{ user.noHp }}</span>
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div>
        <div class="box-medsos mb-3">
          <div class="row">
            <div class="col-md-3">
              <i class="fab fa-instagram-square"></i>
              <a
                :href="`https://www.instagram.com/${user.instagram}`"
                target="_blank"
                ><span>{{ user.instagram }}</span></a
              >
            </div>
            <div class="col-md-3">
              <i class="fab fa-linkedin"></i>
              <span>{{ user.linkedIn }}</span>
            </div>
            <div class="col-md-3">
              <i class="fab fa-twitter-square"></i>
              <span>{{ user.twitter }}</span>
            </div>
            <div class="col-md-3">
              <i class="fab fa-facebook-square"></i>
              <a
                :href="`https://www.facebook.com/${user.facebook}`"
                target="_blank"
                ><span>{{ user.facebook }}</span></a
              >
            </div>
          </div>
        </div>
      </div>
      <button class="btn btn-primary pill float-right" @click="toEdit">
        Edit Profile
      </button>
    </div>
  </div>
</template>
<script>
import request from "../../mixins/request.vue";
export default {
  mixins: [request],
  data() {
    return {
      user: {
        id: "",
        nama: "",
        email: "",
        alamat: "",
        foto: "",
        institusi: "",
        pekerjaan: "",
        pendidikanTerakhir: "",
        provinsi: "",
        kota: "",
        kecamatan: "",
        tanggalLahir: "",
        tempatLahir: "",
        noHp: "",
        facebook: "",
        instagram: "",
        linkedIn: "",
        twitter: ""
      },
      foto: null
    };
  },
  methods: {
    async GET_USER() {
      const USER = await this.requestGet("/profile");
      console.log(USER);
      this.user.id = USER.id;
      this.user.nama = USER.nama;
      this.user.email = USER.email;
      this.user.alamat = USER.alamat;
      this.user.foto = USER.foto;
      this.user.institusi = USER.institusi;
      this.user.pekerjaan = USER.pekerjaan;
      this.user.pendidikanTerakhir = USER.pendidikanTerakhir;
      this.user.provinsi = USER.provinsi;
      this.user.kota = USER.kota;
      this.user.kecamatan = USER.kecamatan;
      this.user.tanggalLahir = USER.tanggalLahir;
      this.user.tempatLahir = USER.tempatLahir;
      this.user.noHp = USER.noHp;
      this.user.facebook = USER.facebook;
      this.user.instagram = USER.instagram;
      this.user.linkedIn = USER.linkedIn;
      this.user.twitter = USER.twitter;
    },
    toEdit() {
      this.$router.push("profile/edit");
    },
    onFileSelected(e) {
      this.foto = e.target.files[0];
    },
    async upload() {
      try {
        const formData = new FormData();
        formData.append("img", this.foto);
        const reqUpload = await this.$axios.$post("/upload/img", formData);
        console.log(reqUpload);
        this.user.foto = reqUpload.data;

        const UPDATE_USER = await this.$axios.$put(
          `/profile/${this.user.id}`,
          this.user
        );
        console.log(UPDATE_USER);
        await this.$swal({
          icon: "success",
          title: "Success",
          text: "Foto berhasil diupdate",
          timer: "2000"
        });
      } catch (error) {
        return this.$swal({
          type: "error",
          title: "Gagal upload",
          text: error.toString()
        });
      }
    }
  },
  mounted() {
    this.GET_USER();
  }
};
</script>

<style scoped>
.jumbotron {
  position: relative;
  color: #524e4e;
  height: 250px;
  background-position: 50px 150px;
  background: url("https://cdn.wallpapersafari.com/12/28/0objwK.jpg");
  background-size: cover;
}

.profile {
  position: absolute;
  left: 100px;
  bottom: -75px;
}

.box-medsos {
  background-color: rgb(232, 216, 250) !important;
  padding: 10px;
  background-color: white;
  border-radius: 40px;
  margin-left: 300px;
  width: 55%;
}

.box-data {
  background-color: burlywood;
  width: 350px;
}

.text-white {
  position: absolute;
  font-size: 25px;
  color: white;
}
.text-white-2 {
  position: absolute;
  font-size: 18px;
  color: white;
}
img:hover {
  cursor: pointer;
}
.card {
  max-width: 500px;
}

a {
  color: rgb(0, 0, 0);
  text-decoration: none;
}
</style>
