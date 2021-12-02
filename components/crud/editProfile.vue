<template>
  <div>
    <div class="form-edit">
      <form class="mt-4" @submit.prevent="updateUser">
        <div class="form-row">
          <div class="form-group col-md-6">
            <label for="inputEmail4">Nama</label>
            <input
              type="text"
              class="form-control"
              id="inputEmail4"
              placeholder="Nama"
              v-model="user.nama"
            />
          </div>

          <div class="form-group col-md-6">
            <label for="inputEmail4">Email</label>
            <input
              type="email"
              class="form-control"
              id="inputEmail4"
              placeholder="Email"
              v-model="user.email"
            />
          </div>
        </div>
        <div class="form-row">
          <div class="form-group col-md-6">
            <label for="inputTempat">Tempat Lahir</label>
            <input
              type="text"
              class="form-control"
              id="inputTempat"
              v-model="user.tempatLahir"
            />
          </div>
          <div class="form-group col-md-6">
            <label for="inputTanggal">Tanggal Lahir</label>
            <input
              type="date"
              class="form-control"
              id="inputTanggal"
              v-model="user.tanggalLahir"
            />
          </div>
        </div>

        <div class="form-row">
          <div class="form-group col-md-6">
            <label for="inputHP">Nomor HP</label>
            <input
              type="text"
              class="form-control"
              id="inputHP"
              v-model="user.noHp"
            />
          </div>
          <div class="form-group col-md-6">
            <label for="inputPendidikan">Pendidikan Terakhir</label>

            <select
              id="inputPendidikan"
              class="form-control"
              v-model="user.pendidikanTerakhir"
            >
              <option value="" selected disabled>Pendidikan Terakhir</option>
              <option value="SD">SD</option>
              <option value="SMP">SMP</option>
              <option value="SMA">SMA</option>
              <option value="S1">S1</option>
              <option value="S2">S2</option>
            </select>
          </div>
        </div>
        <div class="form-row">
          <div class="form-group col-md-6">
            <label for="inputPekerjaan">Pekerjaan</label>
            <input
              type="text"
              class="form-control"
              id="inputPekerjaan"
              v-model="user.pekerjaan"
            />
          </div>
          <div class="form-group col-md-6">
            <label for="inputInstitusi">Institusi</label>
            <input
              type="text"
              class="form-control"
              id="inputInstitusi"
              v-model="user.institusi"
            />
          </div>
        </div>
        <div class="form-group">
          <label for="inputAddress">Alamat</label>
          <input
            type="text"
            class="form-control"
            id="inputAddress"
            v-model="user.alamat"
          />
        </div>
        <div class="form-row">
          <div class="form-group col-md-4">
            <label for="inputKcm">Kecamatan</label>
            <input
              type="text"
              class="form-control"
              id="inputKcm"
              v-model="user.kecamatan"
            />
          </div>
          <div class="form-group col-md-4">
            <label for="inputKota">Kota</label>
            <input
              type="text"
              class="form-control"
              id="inputKota"
              v-model="user.kota"
            />
          </div>
          <div class="form-group col-md-4">
            <label for="inputProv">Provinsi</label>
            <input
              type="text"
              class="form-control"
              id="inputProv"
              v-model="user.provinsi"
            />
          </div>
        </div>
        <div class="form-row">
          <div class="form-group col-md-3">
            <label for="inputIg">Instagram</label>
            <div class="input-group mb-3">
              <div class="input-group-prepend">
                <span class="input-group-text"
                  ><i class="fab fa-instagram"></i
                ></span>
              </div>
              <input
                type="text"
                id="inputIg"
                class="form-control"
                placeholder="Instagram"
                v-model="user.MediaSocial.instagram"
              />
            </div>
          </div>
          <div class="form-group col-md-3">
            <label for="inputLinked">LinkedIn</label>
            <div class="input-group mb-3">
              <div class="input-group-prepend">
                <span class="input-group-text"
                  ><i class="fab fa-linkedin-in"></i
                ></span>
              </div>
              <input
                type="text"
                id="inputLinked"
                class="form-control"
                placeholder="LinkedIn"
                v-model="user.MediaSocial.linkedIn"
              />
            </div>
          </div>
          <div class="form-group col-md-3">
            <label for="inputtwt">Twitter</label>
            <div class="input-group mb-3">
              <div class="input-group-prepend">
                <span class="input-group-text"
                  ><i class="fab fa-twitter"></i
                ></span>
              </div>
              <input
                type="text"
                id="inputtwt"
                class="form-control"
                placeholder="Twitter"
                v-model="user.MediaSocial.twitter"
              />
            </div>
          </div>
          <div class="form-group col-md-3">
            <label for="inputFb">Facebook</label>
            <div class="input-group mb-3">
              <div class="input-group-prepend">
                <span class="input-group-text"
                  ><i class="fab fa-facebook-f"></i
                ></span>
              </div>
              <input
                type="text"
                id="inputFb"
                class="form-control"
                placeholder="Facebook"
                v-model="user.MediaSocial.facebook"
              />
            </div>
          </div>
        </div>
        <button type="submit" class="btn btn-primary">Simpan</button>
      </form>
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
        MediaSocial: {
          facebook: "#",
          instagram: "#",
          linkedIn: "#",
          twitter: "#"
        }
      }
    };
  },
  layout: "profile",
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
      this.user.MediaSocial.facebook = USER.MediaSocial.facebook;
      this.user.MediaSocial.instagram = USER.MediaSocial.instagram;
      this.user.MediaSocial.linkedIn = USER.MediaSocial.linkedin;
      this.user.MediaSocial.twitter = USER.MediaSocial.twitter;
    },
    async updateUser() {
      try {
        const UPDATE_USER = await this.$axios.$put(
          `/profile/${this.user.id}`,
          this.user
        );
        console.log(UPDATE_USER);
        await this.$swal({
          icon: "success",
          title: "Success",
          text: "Profile berhasil diupdate",
          timer: "2000"
        });
        this.$router.push("/profile");
        this.$emit("refreshData");
      } catch (error) {
        this.$swal({
          icon: "danger",
          title: "Waahhh",
          text: "Profile gagal diupdate"
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
.form-edit {
  width: 50%;
}
</style>
