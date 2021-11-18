<template>
  <div>
    <div
      class="d-flex justify-content-around align-items-center flex-wrap"
      v-if="$auth.user.status == 'user'"
    >
      <a
        type="button"
        class="btn btn-secondary pill btn-sm mt-1 arrow"
        data-toggle="modal"
        :data-target="`#${namaKelas}`"
      >
        <span>Detail Kelas</span>
      </a>
      <button @click="confirmGabung" class="btn btn-primary btn-sm pill arrow">
        <span>Gabung kelas</span>
      </button>
    </div>
    <div class="float-right">
      <items-buttonEdit
        :id="id"
        :kode="kode"
        :nama="nama"
        :deskripsi="deskripsi"
        :tanggalMulai="tanggalMulai"
        :tanggalSelesai="tanggalSelesai"
        :foto="foto"
        v-if="$auth.loggedIn && $auth.user.status == 'admin'"
      />
    </div>

    <div
      :id="`${namaKelas}`"
      class="modal fade"
      tabindex="-1"
      role="dialog"
      aria-labelledby="myLargeModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-lg large">
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
            <div class="row">
              <div class="col-lg-6 text-center">
                <img
                  :src="foto"
                  :alt="namaKelas"
                  width="400px"
                  height="300px"
                />
              </div>
              <div class="col-lg-6">
                <h4>{{ nama }} - {{ kode }}</h4>
                <ul
                  class="nav nav-pills pt-2 mb-3"
                  id="pills-tab"
                  role="tablist"
                >
                  <li class="nav-item" role="presentation">
                    <a
                      class="nav-link active"
                      :id="`pills-${namaKelas}-desc-tabs`"
                      data-toggle="pill"
                      :href="`#pills-${namaKelas}-desc`"
                      role="tab"
                      aria-controls="pills-home"
                      aria-selected="true"
                      >Deskripsi</a
                    >
                  </li>
                  <li class="nav-item" role="presentation">
                    <a
                      class="nav-link"
                      :id="`pilsl-${namaKelas}-jadwal-tabs`"
                      data-toggle="pill"
                      :href="`#pills-${namaKelas}-jadwal`"
                      role="tab"
                      aria-controls="pills-profile"
                      aria-selected="false"
                      >Jadwal</a
                    >
                  </li>
                </ul>
                <div class="tab-content" id="pills-tabContent">
                  <div
                    class="tab-pane fade show active"
                    :id="`pills-${namaKelas}-desc`"
                    role="tabpanel"
                    aria-labelledby="pills-home-tab"
                  >
                    <p class="mt-3 line-height">{{ deskripsi }}</p>
                  </div>
                  <div
                    class="tab-pane fade"
                    :id="`pills-${namaKelas}-jadwal`"
                    role="tabpanel"
                    aria-labelledby="pills-profile-tab"
                  >
                    <table class="mt-3">
                      <tbody>
                        <tr>
                          <td class="pb-2" width="80">Mulai :</td>
                          <td class="pb-2">{{ tanggalMulai }}</td>
                        </tr>
                        <tr>
                          <td>Selesai :</td>
                          <td>{{ tanggalSelesai }}</td>
                        </tr>
                      </tbody>
                    </table>
                  </div>
                </div>
              </div>
            </div>
            <div class="modal-footer">
              <button
                type="button"
                class="btn btn-secondary pill"
                data-dismiss="modal"
              >
                Tutup
              </button>
              <button
                @click="confirmGabung"
                type="button"
                class="btn btn-primary pill"
              >
                Gabung kelas
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    id: { type: Number },
    kode: { type: String },
    nama: { type: String },
    deskripsi: { type: String },
    tanggalMulai: { type: String },
    tanggalSelesai: { type: String },
    foto: { type: String }
  },
  computed: {
    //nama kelas tanpa spasi
    namaKelas() {
      return this.nama.toLowerCase().replace(/ /g, "-");
    }
  },
  methods: {
    async confirmGabung() {
      this.$swal({
        title: "Apakah kamu yakin?",
        text: `Ingin bergabung dengan kelas ${this.namaKelas}.`,
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#3085d6",
        cancelButtonColor: "#d33",
        confirmButtonText: "Ya, bergabung"
      }).then(result => {
        if (result.isConfirmed) {
          const payload = {
            classId: this.id
          };
          const JOIN_KELAS = this.$axios.$post("/join", payload);
          console.log(JOIN_KELAS);
          this.$swal(
            "Berhasil!",
            `Kamu berhasil bergabung dengan kelas ${this.namaKelas}.`,
            "success"
          );
        }
      });
    }
  }
};
</script>

<style scoped>
.large {
  margin-top: 100px;
  width: 1000px;
}
.pill {
  border-radius: 30px;
}
.line-height {
  margin-right: 20px;
  text-align: justify;
  line-height: 23px;
}

.btn {
  padding: 7px 20px 7px 20px;
}
span {
  font-size: 0.9em;
}

.arrow span {
  cursor: pointer;
  display: inline-block;
  position: relative;
  transition: 0.5s;
}

.arrow span:after {
  content: "\00bb";
  position: absolute;
  opacity: 0;
  top: 0;
  right: -20px;
  transition: 0.5s;
}

.arrow:hover span {
  padding-right: 15px;
}

.arrow:hover span:after {
  opacity: 1;
  right: 0;
}
</style>
