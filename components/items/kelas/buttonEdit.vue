<template>
  <div>
    <!-- Button trigger modal -->
    <button
      class="btn btn-primary btn-sm pill"
      type="button"
      data-toggle="modal"
      :data-target="`#edit${id}`"
    >
      Edit Kelas
    </button>

    <!-- Modal -->
    <div
      class="modal fade"
      :id="`edit${id}`"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalCenterTitle"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLongTitle">
              Edit Kelas
            </h5>
            <button
              type="button"
              class="close"
              data-dismiss="modal"
              aria-label="Close"
            >
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <form @submit.prevent="updateKelas">
            <div class="modal-body">
              <input-type
                name="Kode Kelas"
                :value="kode"
                @get="val => (kode = val)"
              />
              <input-type
                name="Nama Kelas"
                :value="nama"
                @get="val => (nama = val)"
              />
              <input-type
                name="Deskripsi Kelas"
                :value="deskripsi"
                @get="val => (deskripsi = val)"
              />
              <input-type
                type="date"
                name="Tanggal Mulai"
                :value="tanggalMulai"
                @get="val => (tanggalMulai = val)"
              />
              <input-type
                type="date"
                name="Tanggal Selesai"
                :value="tanggalSelesai"
                @get="val => (tanggalSelesai = val)"
              />
              <input-type
                name="Foto Kelas"
                :value="foto"
                @get="val => (foto = val)"
              />
            </div>
            <div class="modal-footer">
              <button
                type="button"
                class="btn btn-secondary"
                data-dismiss="modal"
              >
                Back
              </button>
              <button type="submit" class="btn btn-primary">
                Edit
              </button>
            </div>
          </form>
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
  methods: {
    async updateKelas() {
      try {
        const payload = {
          id: this.id,
          kodeKelas: this.kode,
          namaKelas: this.nama,
          deskripsiKelas: this.deskripsi,
          tanggalMulai: this.tanggalMulai,
          tanggalSelesai: this.tanggalSelesai,
          fotoKelas: this.foto
        };
        const UPDATE_KELAS = await this.$axios.$put(
          `/kelas/${payload.id}`,
          payload
        );
        console.log(UPDATE_KELAS);
        this.$swal({
          icon: "success",
          title: "Success",
          text: "Kelas berhasil diupdate",
          timer: "2000"
        });
        $(".modal").modal("hide");
        this.$emit("refreshData");
      } catch (error) {
        this.$swal({
          icon: "danger",
          title: "Waahhh",
          text: "Kelas gagal diupdate"
        });
      }
    }
  }
};
</script>

<style scoped>
.pill {
  border-radius: 30px;
}
</style>
