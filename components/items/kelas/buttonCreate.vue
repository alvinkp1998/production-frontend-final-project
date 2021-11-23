<template>
  <div>
    <!-- Button trigger modal -->
    <button
      class="btn btn-primary px-4 py-3 position-fixed"
      type="button"
      style="right:20px;bottom:80px;z-index:5;border-radius: 30px"
      data-toggle="modal"
      data-target="#modalCreate"
    >
      Tambah Kelas
    </button>

    <!-- Modal -->
    <div
      class="modal fade"
      id="modalCreate"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalCenterTitle"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLongTitle">
              Tambah Kelas
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
          <form @submit.prevent="tambahKelas">
            <div class="modal-body">
              <input-type
                name="Kode Kelas"
                @get="val => (detailClass.kodeKelas = val)"
              />
              <input-type
                name="Nama Kelas"
                @get="val => (detailClass.namaKelas = val)"
              />
              <input-type
                name="Deskripsi Kelas"
                @get="val => (detailClass.deskripsiKelas = val)"
              />
              <input-type
                type="date"
                name="Tanggal Mulai"
                @get="val => (detailClass.tanggalMulai = val)"
              />
              <input-type
                type="date"
                name="Tanggal Selesai"
                @get="val => (detailClass.tanggalSelesai = val)"
              />
              <input-type
                name="Foto Kelas"
                @get="val => (detailClass.fotoKelas = val)"
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
      detailClass: {
        kodeKelas: "",
        namaKelas: "",
        tanggalMulai: "",
        tanggalSelesai: "",
        deskripsiKelas: "",
        fotoKelas: ""
      }
    };
  },
  methods: {
    async tambahKelas() {
      try {
        const payload = this.detailClass;
        const TAMBAH_KELAS = await this.$axios.$post("/kelas", payload);
        console.log(TAMBAH_KELAS);
        this.$swal({
          icon: "success",
          title: "Success",
          text: "Kelas berhasil ditambah",
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
          text: "Kelas gagal ditambah"
        });
      }
    }
  }
};
</script>
