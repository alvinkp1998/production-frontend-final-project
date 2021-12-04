<template>
  <div>
    <div class="container">
      <div class="h2 text-center">Presensi Kelas</div>
      <hr />
      <ul class="nav" v-for="kelas in listClass" :key="kelas.id">
        <div>
          <li>
            <a
              class="nav-link"
              data-toggle="collapse"
              :href="`#kelas${kelas.id}`"
              ><h3>
                <i class="fas fa-caret-right"></i> {{ kelas.namaKelas }} -
                {{ kelas.kodeKelas }}
              </h3></a
            >
          </li>
        </div>
        <div class="container">
          <div class="card collapse" :id="`kelas${kelas.id}`">
            <div class="card-body">
              <ul
                class="nav nav-tabs mb-2"
                v-for="sesi in kelas.Sessions"
                :key="sesi.id"
              >
                <li class="nav-item">
                  <a
                    class="nav-link mb-2 "
                    :href="`#sesi${sesi.id}`"
                    data-toggle="collapse"
                    ><h5>Sesi {{ sesi.urutanSesi }}</h5></a
                  >
                </li>
                <div class="container-fluid">
                  <div :id="`sesi${sesi.id}`" class="collapse">
                    <hr />
                    <h4>
                      <i class="fas fa-info-circle"></i> Informasi Sesi
                      {{ sesi.urutanSesi }}
                    </h4>
                    <hr />
                    <div class="row">
                      <div class="col-2"><h5>Nama Sesi</h5></div>
                      <div class="col-10">
                        <p>{{ sesi.namaSesi }}</p>
                      </div>
                    </div>
                    <div class="row">
                      <div class="col-2"><h5>Waktu Mulai</h5></div>
                      <div class="col-10">
                        <p>{{ sesi.waktuMulai }}</p>
                      </div>
                    </div>
                    <div class="row">
                      <div class="col-2"><h5>Waktu Selesai</h5></div>
                      <div class="col-10">
                        <p>{{ sesi.waktuSelesai }}</p>
                      </div>
                    </div>
                    <div class="row mb-2">
                      <div class="col-2"><h5>Status</h5></div>
                      <div class="col-10">
                        <span v-if="sesi.absen === 'Sudah Absen'" class="done">
                          {{ sesi.absen }} <i class="fas fa-check-circle"></i>
                        </span>
                        <span v-else class="notYet">
                          {{ sesi.absen }} <i class="fas fa-times-circle"></i>
                        </span>
                      </div>
                    </div>
                    <p style="font-style: italic">
                      Note: Presensi dilakukan saat sesi sudah dibuka, silahkan
                      presensi dengan menginputkan kode sesi yang diberikan
                      setelah sesi selesai.
                    </p>
                    <div class="kode mb-2 mt-3 pt-2">
                      <span class="box-kode">Masukkan Kode Sesi</span>
                    </div>
                    <form
                      @submit.prevent="
                        submitPresensi(sesi.kodeSesi, kelas.kodeKelas)
                      "
                    >
                      <div class="row">
                        <div class="col-md-10">
                          <input
                            type="text"
                            class="form-control"
                            placeholder="Masukkan Kode Sesi"
                            required
                            v-model="kodeSesi"
                          />
                        </div>
                        <div class="col-md-2">
                          <button class="btn btn-primary btn-block">
                            <i class="fas fa-key"></i> Kode
                          </button>
                        </div>
                      </div>
                    </form>
                  </div>
                </div>
              </ul>
            </div>
          </div>
        </div>
      </ul>
    </div>
  </div>
</template>

<script>
import request from "../../mixins/request.vue";
export default {
  mixins: [request],
  data() {
    return {
      listClass: [],
      kodeSesi: ""
    };
  },
  methods: {
    async GET_PRESENSI() {
      try {
        const PRESENSI = await this.requestGet("/presensi");
        console.log(PRESENSI);
        this.listClass = PRESENSI.data;
      } catch (error) {
        console.log(error);
      }
    },
    async submitPresensi(kodeSesi, kodeKelas) {
      try {
        if (this.kodeSesi === kodeSesi) {
          const payload = {
            kodeSesi: kodeSesi,
            kodeKelas: kodeKelas
          };
          const response = await this.$axios.post("/presensi", payload);
          console.log(response);
          this.$swal({
            title: "Kode Berhasil",
            text: "Kamu berhasil Presensi",
            icon: "success",
            timer: 2000,
            buttons: false
          }).then(() => {
            this.kodeSesi = "";
            this.GET_PRESENSI();
          });
        } else {
          this.$swal({
            title: "Kode Salah",
            text: "Gagal Presensi",
            icon: "error",
            timer: 2000,
            buttons: false
          });
        }
      } catch (error) {
        console.log(error);
      }
    }
  },
  mounted() {
    this.GET_PRESENSI();
  }
};
</script>

<style scoped>
.card {
  border-radius: 20px;
  border: 2px solid rgb(72, 42, 88);
}

a {
  color: rgb(48, 47, 47);
}

.row {
  padding: 0;
  margin: 0;
}

.box-kode {
  color: white;
  padding: 10px;
  background-color: rgb(131, 75, 131);
}

.done {
  color: white;
  background-color: green;
  padding: 10px;
}

.notYet {
  color: white;
  background-color: rgb(247, 0, 0);
  padding: 10px;
}
</style>
