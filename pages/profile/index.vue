<template>
  <div>
    <div>
      <div class="jumbotron jumbotron-fluid">
        <div class="container profile">
          <div class="row">
            <div class="col-md-2">
              <img
                src="https://w7.pngwing.com/pngs/81/570/png-transparent-profile-logo-computer-icons-user-user-blue-heroes-logo-thumbnail.png"
                class="rounded-circle"
                alt="Cinque Terre"
                width="170px"
                height="170px"
              />
            </div>
            <div class="col-md-4">
              <span class="text-white ml-3 mt-4 ">{{ user.nama }}</span>
              <span class="text-white-2 ml-3 mt-5 pt-2"
                >{{ user.pekerjaan }} at {{ user.institusi }}</span
              >
            </div>
            <div class="col-md-6">
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
        <div class="box-medsos float-left mb-3">
          <div class="row">
            <div class="col-md-3">
              <i class="fab fa-instagram-square"></i>
              <span>{{ user.MediaSocial.instagram }}</span>
            </div>
            <div class="col-md-3">
              <i class="fab fa-linkedin"></i>
              <span>{{ user.MediaSocial.linkedIn }}</span>
            </div>
            <div class="col-md-3">
              <i class="fab fa-twitter-square"></i>
              <span>{{ user.MediaSocial.twitter }}</span>
            </div>
            <div class="col-md-3">
              <i class="fab fa-facebook-square"></i>
              <span>{{ user.MediaSocial.facebook }}</span>
            </div>
          </div>
        </div>
        <!-- <crud-editProfile
          :id="user.id"
          :nama="user.nama"
          :tempatLahir="user.tempatLahir"
          :tanggalLahir="user.tanggalLahir"
          :noHp="user.noHp"
          :pendidikan="user.pendidikanTerakhir"
          :institusi="user.institusi"
          :pekerjaan="user.pekerjaan"
          @refreshData="GET_USER"
        /> -->
        <button class="btn btn-primary pill float-right" @click="toEdit">
          Edit Profile
        </button>
      </div>
      <div class="card" style="clear: both;">
        <div class="card-body"></div>
      </div>
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
        MediaSocial: {
          facebook: "",
          instagram: "",
          linkedIn: "",
          twitter: ""
        }
      }
    };
  },
  layout: "profile",
  methods: {
    async GET_USER() {
      const USER = await this.requestGet("/profile");
      console.log(USER);
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
      this.user.MediaSocial.facebook = USER.MediaSocial.facebook;
      this.user.MediaSocial.instagram = USER.MediaSocial.instagram;
      this.user.MediaSocial.linkedIn = USER.MediaSocial.linkedin;
      this.user.MediaSocial.twitter = USER.MediaSocial.twitter;
    },
    toEdit() {
      this.$router.push("profile/edit");
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
  padding: 10px;
  background-color: white;
  border-radius: 40px;
  margin-left: 300px;
  width: 55%;
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

.card-body {
  width: 400px;
  /* background-color: blue; */
}
</style>
