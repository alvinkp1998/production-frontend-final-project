<template>
  <div>
    <!-- Button trigger modal -->
    <button
      class="btn btn-primary btn-sm pill mt-3 mr-1"
      type="button"
      data-toggle="modal"
      :data-target="`#modalEditMateri${id}`"
    >
      Edit
    </button>

    <!-- Modal -->
    <div
      class="modal fade"
      :id="`modalEditMateri${id}`"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalCenterTitle"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLongTitle">
              Edit Materi
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
          <form @submit.prevent="updateMateri">
            <div class="modal-body">
              <input-type
                name="Nama Materi"
                :value="namaMateri"
                @get="val => (namaMateri = val)"
              />

              <input-type
                type="file"
                name="file"
                :value="file"
                @get="val => (file = val)"
              />
              <input-type
                name="Jenis Materi"
                :value="jenisMateri"
                @get="val => (jenisMateri = val)"
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
    id: Number,
    namaMateri: String,
    file: String,
    jenisMateri: String
  },
  // data() {
  //   return {
  //     docs: null,
  //     video: null
  //   };
  // },
  methods: {
    async updateMateri() {
      try {
        const payload = {
          namaMateri: this.namaMateri,
          file: this.file,
          jenisMateri: this.jenisMateri
        };
        const UPDATE_MATERI = await this.$axios.$put(
          `/materi/${this.id}`,
          payload
        );
        console.log(UPDATE_MATERI);
        this.$swal({
          icon: "success",
          title: "Success",
          text: "Materi berhasil diupdate",
          timer: "2000"
        });
        $(".modal").modal("hide");
        this.$emit("refreshData");
      } catch (error) {
        this.$swal({
          icon: "danger",
          title: "Waahhh",
          text: "Materi gagal diupdate"
        });
      }
    }
    // onDocsSelected(e) {
    //   this.docs = e.target.files[0];
    // },
    // onVideoSelected(e) {
    //   this.video = e.target.files[0];
    // },
    // async uploadMateriDocs() {
    //   try {
    //     const formData = new FormData();
    //     formData.append("docs", this.docs);
    //     const reqUpload = await this.$axios.$post("/upload/docs", formData);
    //     console.log(reqUpload);
    //     this.file = reqUpload;
    //   } catch (error) {
    //     return this.$swal({
    //       type: "error",
    //       title: "Gagal upload",
    //       text: error.toString()
    //     });
    //   }
    // },
    // async uploadVideo() {
    //   try {
    //     const formData = new FormData();
    //     formData.append("video", this.video);
    //     const reqUpload = await this.$axios.$post("/upload/videos", formData);
    //     console.log(reqUpload);
    //     this.file = reqUpload.data;
    //   } catch (error) {
    //     return this.$swal({
    //       type: "error",
    //       title: "Gagal upload",
    //       text: error.toString()
    //     });
    //   }
    // }
  }
};
</script>

<style scoped>
.pill {
  border-radius: 30px;
}
</style>
