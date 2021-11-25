<template>
  <div>
    <!-- Button trigger modal -->
    <button
      class="btn btn-primary px-4 py-3 position-fixed"
      type="button"
      style="right:20px;bottom:80px;z-index:5;border-radius: 30px"
      data-toggle="modal"
      data-target="#modalCreateMateri"
    >
      Tambah Materi
    </button>

    <!-- Modal -->
    <div
      class="modal fade"
      id="modalCreateMateri"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalCenterTitle"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLongTitle">
              Tambah Materi
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
          <form @submit.prevent="tambahMateri">
            <div class="modal-body">
              <input-type
                name="Nama Materi"
                @get="val => (detailMateri.namaMateri = val)"
              />
              <input-type
                type="file"
                name="file"
                @get="val => (detailMateri.file = val)"
              />
              <input-type
                name="Jenis Materi"
                @get="val => (detailMateri.jenisMateri = val)"
              />
              <!-- 
              <div class="row">
                <div class="col-md-3">
                  <label class="text-capitalize" for="">Jenis Materi</label>
                </div>
                <div class="col-md-9">
                  <input
                    type="radio"
                    id="powerpoint"
                    :value="detailMateri.jenisMaterippt"
                    name="jenisMateri"
                  />
                  <label for="powerpoint">Power Point</label>

                  <input
                    type="radio"
                    id="recording"
                    :value="detailMateri.jenisMateri"
                    name="jenisMateri"
                  />
                  <label for="recording">recording</label>
                </div>
              </div> -->
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
      detailMateri: {
        namaMateri: "",
        file: "",
        jenisMateri: "",
        // jenisMateri: "recording",
        // jenisMaterippt: "powerpoint",
        SessionId: this.$route.params.sessionId
      }
    };
  },
  methods: {
    async tambahMateri() {
      try {
        const payload = this.detailMateri;
        const TAMBAH_MATERI = await this.$axios.$post(`/materi`, payload);
        console.log(TAMBAH_MATERI);
        this.$swal({
          icon: "success",
          title: "Success",
          text: "Materi berhasil ditambah",
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
          text: "Materi gagal ditambah"
        });
      }
    }
  }
};
</script>
