<template>
  <div>
    <!-- Button trigger modal -->
    <button
      class="btn btn-primary px-4 py-3 position-fixed"
      type="button"
      style="right:20px;bottom:80px;z-index:5;border-radius: 30px"
      data-toggle="modal"
      data-target="#modalCreateSesi"
    >
      Tambah Sesi
    </button>

    <!-- Modal -->
    <div
      class="modal fade"
      id="modalCreateSesi"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalCenterTitle"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLongTitle">
              Tambah Sesi
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
          <form @submit.prevent="tambahSesi">
            <div class="modal-body">
              <input-type
                name="Nama Sesi"
                @get="val => (detailSesi.namaSesi = val)"
              />
              <input-type
                name="Urutan Sesi"
                @get="val => (detailSesi.urutanSesi = val)"
              />
              <input-type
                name="Kode Sesi"
                @get="val => (detailSesi.kodeSesi = val)"
              />
              <input-type
                type="date"
                name="Waktu Mulai"
                @get="val => (detailSesi.waktuMulai = val)"
              />
              <input-type
                type="date"
                name="Waktu Selesai"
                @get="val => (detailSesi.waktuSelesai = val)"
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
                Tambah
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
  data() {
    return {
      detailSesi: {
        namaSesi: "",
        urutanSesi: "",
        waktuMulai: "",
        waktuSelesai: "",
        kodeSesi: "",
        ClassId: this.$route.params.classId
      }
    };
  },
  methods: {
    async tambahSesi() {
      try {
        const payload = this.detailSesi;
        const TAMBAH_SESI = await this.$axios.$post(`/sesi`, payload);
        console.log(TAMBAH_SESI);
        this.$swal({
          icon: "success",
          title: "Success",
          text: "Sesi berhasil ditambah",
          timer: "2000"
        });
        $(".modal").modal("hide");
        this.$emit("refreshData");

        // Belum untuk hapus inoutan saat ingin memasukkan kembali datanya
        console.log(payload);
      } catch (error) {
        this.$swal({
          icon: "danger",
          title: "Waahhh",
          text: "Sesi gagal ditambah"
        });
      }
    }
  }
};
</script>
