<template>
  <div>
    <!-- Button trigger modal -->
    <button
      class="btn btn-primary btn-sm pill mt-3 mr-1"
      data-toggle="modal"
      :data-target="`#modalEditSesi${id}`"
    >
      Edit
    </button>

    <!-- Modal -->
    <div
      class="modal fade"
      :id="`modalEditSesi${id}`"
      role="dialog"
      aria-labelledby="exampleModalCenterTitle"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLongTitle">
              Edit Sesi
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
          <form @submit.prevent="updateSesi">
            <div class="modal-body">
              <input-type
                name="Nama Sesi"
                :value="namaSesi"
                @get="val => (namaSesi = val)"
              />
              <input-type
                name="Urutan Sesi"
                :value="urutanSesi"
                @get="val => (urutanSesi = val)"
              />
              <input-type
                name="Kode Sesi"
                :value="kodeSesi"
                @get="val => (kodeSesi = val)"
              />
              <input-type
                type="date"
                name="Waktu Mulai"
                :value="waktuMulai"
                @get="val => (waktuMulai = val)"
              />
              <input-type
                type="date"
                name="Waktu Selesai"
                :value="waktuSelesai"
                @get="val => (waktuSelesai = val)"
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
    namaSesi: { type: String },
    urutanSesi: { type: Number },
    waktuMulai: { type: String },
    waktuSelesai: { type: String },
    kodeSesi: String
  },
  methods: {
    async updateSesi() {
      try {
        const payload = {
          namaSesi: this.namaSesi,
          urutanSesi: this.urutanSesi,
          waktuMulai: this.waktuMulai,
          waktuSelesai: this.waktuSelesai,
          kodeSesi: this.kodeSesi
        };
        const UPDATE_SESI = await this.$axios.$put(`/sesi/${this.id}`, payload);
        console.log(UPDATE_SESI);
        this.$swal({
          icon: "success",
          title: "Success",
          text: "Sesi berhasil diupdate",
          timer: "2000"
        });
        $(".modal").modal("hide");
        this.$emit("refreshData");
      } catch (error) {
        this.$swal({
          icon: "danger",
          title: "Waahhh",
          text: "Sesi gagal diupdate"
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
