<template>
  <div>
    <div
      class="d-flex justify-content-around align-items-center flex-wrap"
      v-if="!$auth.loggedIn || $auth.user.status == 'user'"
    >
      <a
        type="button"
        class="btn btn-secondary pill btn-sm mt-1 arrow"
        data-toggle="modal"
        :data-target="`#${namaKelas}`"
      >
        <span>Detail Kelas</span>
      </a>
      <div class="btn-group dropright">
        <button
          class="btn btn-primary btn-sm pill dropdown-toggle"
          data-toggle="dropdown"
        >
          <span>Gabung kelas</span>
        </button>
        <div class="dropdown-menu">
          <a class="dropdown-item" @click="confirmGabungTutor"
            >Join Sebagai Tutor</a
          >
          <a class="dropdown-item" @click="confirmGabungStudent"
            >Join Sebagai Student</a
          >
          <a class="dropdown-item" @click="confirmGabungFasilitator"
            >Join Sebagai Fasilitator</a
          >
        </div>
      </div>
      <!-- <button class="btn btn-primary btn-sm pill arrow" @click="confirmGabung">
        <span>Gabung kelas</span>
      </button> -->
    </div>
    <button
      class="btn btn-primary pill"
      @click="toClassAdmin"
      v-if="$auth.loggedIn && $auth.user.status == 'admin'"
    >
      Isi Kelas
    </button>
    <div class="float-right">
      <items-kelas-buttonEdit
        :id="id"
        :kode="kode"
        :nama="nama"
        :deskripsi="deskripsi"
        :tanggalMulai="tanggalMulai"
        :tanggalSelesai="tanggalSelesai"
        :foto="foto"
        @refreshData="$emit('refreshData')"
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
                  <li class="nav-item" role="presentation">
                    <a
                      class="nav-link"
                      :id="`pilsl-${namaKelas}-materi-tabs`"
                      data-toggle="pill"
                      :href="`#pills-${namaKelas}-materi`"
                      role="tab"
                      aria-controls="pills-profile"
                      aria-selected="false"
                      >Materi</a
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
                  <div
                    class="tab-pane fade"
                    :id="`pills-${namaKelas}-materi`"
                    role="tabpanel"
                    aria-labelledby="pills-profile-tab"
                  >
                    asdsa
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
    // async confirmGabung() {
    //   try {
    //     if (this.$auth.loggedIn) {
    //       const yakin = await this.$swal({
    //         title: "Apakah kamu yakin?",
    //         text: `Ingin bergabung dengan kelas ${this.namaKelas}.`,
    //         icon: "question",
    //         showCancelButton: true,
    //         confirmButtonColor: "#3085d6",
    //         cancelButtonColor: "#d33",
    //         confirmButtonText: "Ya, bergabung"
    //       });
    //       if (yakin.isConfirmed) {
    //         const payload = {
    //           classId: this.id,
    //           roleId: 3
    //         };
    //         const JOIN_KELAS = await this.$axios.$post("/join", payload);
    //         console.log(JOIN_KELAS);
    //         this.$swal(
    //           "Berhasil!",
    //           `Kamu berhasil bergabung dengan kelas ${this.namaKelas}.`,
    //           "success"
    //         );
    //       }
    //     } else {
    //       await this.$swal({
    //         icon: "warning",
    //         title: "Tidak bisa bergabung ke kelas",
    //         text: "Anda harus login terlebih dahulu"
    //       });
    //       this.$router.push("/login");
    //     }
    //   } catch (error) {
    //     this.$swal({
    //       icon: "warning",
    //       title: "Gagal",
    //       text: `Anda sudah bergabung dengan kelas ${this.namaKelas}`
    //     });
    //   }
    // },
    async confirmGabungTutor() {
      try {
        if (this.$auth.loggedIn) {
          const yakin = await this.$swal({
            title: "Apakah kamu yakin?",
            text: `Ingin bergabung sebagai tutor pada kelas ${this.namaKelas}.`,
            icon: "question",
            showCancelButton: true,
            confirmButtonColor: "#3085d6",
            cancelButtonColor: "#d33",
            confirmButtonText: "Ya, bergabung"
          });
          if (yakin.isConfirmed) {
            const payload = {
              classId: this.id,
              roleId: 1
            };
            const JOIN_KELAS = await this.$axios.$post("/join", payload);
            console.log(JOIN_KELAS);
            this.$swal(
              "Berhasil!",
              `Kamu berhasil bergabung dengan kelas ${this.namaKelas}.`,
              "success"
            );
          }
        } else {
          await this.$swal({
            icon: "warning",
            title: "Tidak bisa bergabung ke kelas",
            text: "Anda harus login terlebih dahulu"
          });
          this.$router.push("/login");
        }
      } catch (error) {
        this.$swal({
          icon: "warning",
          title: "Gagal",
          text: `Anda sudah bergabung dengan kelas ${this.namaKelas}`
        });
      }
    },
    async confirmGabungFasilitator() {
      try {
        if (this.$auth.loggedIn) {
          const yakin = await this.$swal({
            title: "Apakah kamu yakin?",
            text: `Ingin bergabung sebagai fasilitator pada kelas ${this.namaKelas}.`,
            icon: "question",
            showCancelButton: true,
            confirmButtonColor: "#3085d6",
            cancelButtonColor: "#d33",
            confirmButtonText: "Ya, bergabung"
          });
          if (yakin.isConfirmed) {
            const payload = {
              classId: this.id,
              roleId: 2
            };
            const JOIN_KELAS = await this.$axios.$post("/join", payload);
            console.log(JOIN_KELAS);
            this.$swal(
              "Berhasil!",
              `Kamu berhasil bergabung dengan kelas ${this.namaKelas}.`,
              "success"
            );
          }
        } else {
          await this.$swal({
            icon: "warning",
            title: "Tidak bisa bergabung ke kelas",
            text: "Anda harus login terlebih dahulu"
          });
          this.$router.push("/login");
        }
      } catch (error) {
        this.$swal({
          icon: "warning",
          title: "Gagal",
          text: `Anda sudah bergabung dengan kelas ${this.namaKelas}`
        });
      }
    },
    async confirmGabungStudent() {
      try {
        if (this.$auth.loggedIn) {
          const yakin = await this.$swal({
            title: "Apakah kamu yakin?",
            text: `Ingin bergabung sebagai student pada kelas ${this.namaKelas}.`,
            icon: "question",
            showCancelButton: true,
            confirmButtonColor: "#3085d6",
            cancelButtonColor: "#d33",
            confirmButtonText: "Ya, bergabung"
          });
          if (yakin.isConfirmed) {
            const payload = {
              classId: this.id,
              roleId: 3
            };
            const JOIN_KELAS = await this.$axios.$post("/join", payload);
            console.log(JOIN_KELAS);
            this.$swal(
              "Berhasil!",
              `Kamu berhasil bergabung dengan kelas ${this.namaKelas}.`,
              "success"
            );
          }
        } else {
          await this.$swal({
            icon: "warning",
            title: "Tidak bisa bergabung ke kelas",
            text: "Anda harus login terlebih dahulu"
          });
          this.$router.push("/login");
        }
      } catch (error) {
        this.$swal({
          icon: "warning",
          title: "Gagal",
          text: `Anda sudah bergabung dengan kelas ${this.namaKelas}`
        });
      }
    },
    toClassAdmin() {
      this.$router.push(`/kelasku/${this.namaKelas}/${this.id}`);
    },
    toEditPage() {
      this.$router.push(`/admin/${this.id}/editClass`);
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

.dropdown-item {
  cursor: pointer;
}
</style>
