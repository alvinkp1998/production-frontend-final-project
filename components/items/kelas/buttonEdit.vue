<template>
  <div>
    <!-- Button trigger modal -->
    <button
      class="btn btn-primary btn-sm pill"
      type="button"
      data-toggle="modal"
      data-target="#modalEdit"
    >
      Edit Kelas
    </button>

    <!-- Modal -->
    <div
      class="modal fade"
      id="modalEdit"
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
              <input-type name="Kode Kelas" v-model="kode" />
              <input-type name="Nama Kelas" v-model="nama" />
              <input-type name="Deskripsi Kelas" v-model="deskripsi" />
              <input-type
                type="date"
                name="Tanggal Mulai"
                v-model="tanggalMulai"
              />
              <input-type
                type="date"
                name="Tanggal Selesai"
                v-model="tanggalSelesai"
              />
              <input-type name="Foto Kelas" v-model="foto" />
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
        const UPDATE_KELAS = await this.$axios.$put("/kelas/", this.id);
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
