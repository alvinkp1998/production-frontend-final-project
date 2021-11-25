<template>
  <div>
    <div class="card shadow-lg">
      <div v-if="$auth.loggedIn && $auth.user.status == 'admin'">
        <span class="text-right bigger-text float-right" @click="confirmDelete"
          >&times;</span
        >
      </div>

      <div class="text-center">
        <img
          class="card-img-top gambar "
          :src="foto"
          alt="Card image cap"
          width="100%"
          height="170px"
        />
      </div>
      <div class="card-body">
        <h5 class="card-text text text-center">{{ nama }}</h5>
      </div>
      <class-modal
        :id="id"
        :kode="kode"
        :nama="nama"
        :deskripsi="deskripsi"
        :tanggalMulai="tanggalMulai"
        :tanggalSelesai="tanggalSelesai"
        :foto="foto"
        @refreshData="$emit('refreshData')"
      />
    </div>
  </div>
</template>

<script>
import request from "../../mixins/request.vue";
export default {
  mixins: [request],
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
    async confirmDelete() {
      const confirm = await this.confirm("Menghapus kelas " + this.nama);
      if (confirm.isConfirmed) {
        await this.requestDelete("/kelas/" + this.id);
        this.$emit("refreshData");
      }
    }
  }
};
</script>

<style scoped>
.card {
  max-width: 400px;
  min-width: 150px;
  padding: 1.2em;
  background-color: white;
}

.gambar {
  max-width: 300px;
}

.bigger-text {
  width: 100%;
  cursor: pointer;
  font-size: 26px;
}

/* // Small devices (landscape phones, 576px and up) */
@media (min-width: 576px) {
  .text {
    font-size: 20px;
  }
}

/* // Medium devices (tablets, 768px and up) */
@media (min-width: 768px) {
  .text {
    font-size: 15px;
  }
}

/* // Large devices (desktops, 992px and up) */
@media (min-width: 992px) {
  .text {
    font-size: 14px;
  }
}

/* // Extra large devices (large desktops, 1200px and up) */
@media (min-width: 1200px) {
  .text {
    font-size: 17px;
  }
}
</style>
