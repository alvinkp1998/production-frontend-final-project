<template>
  <div>
    <div class="row ">
      <div
        class="col-lg-3 col-md-6 margintop"
        v-for="item in listClass"
        :key="item.id"
      >
        <class-item
          @refresh="GET_LIST_CLASS"
          :id="item.id"
          :kode="item.kodeKelas"
          :nama="item.namaKelas"
          :deskripsi="item.deskripsiKelas"
          :tanggalMulai="item.tanggalMulai"
          :tanggalSelesai="item.tanggalSelesai"
          :foto="item.fotoKelas"
        />
      </div>
      <items-buttonCreate />
    </div>
  </div>
</template>

<script>
import request from "../../mixins/request.vue";
export default {
  mixins: [request],
  auth: false,
  data() {
    return {
      listClass: []
    };
  },
  methods: {
    async GET_LIST_CLASS() {
      const LIST_CLASS = await this.requestGet("/kelas");
      console.log(LIST_CLASS);
      this.listClass = LIST_CLASS.requestDB;
    }
  },
  mounted() {
    this.GET_LIST_CLASS();
  }
};
</script>

<style scoped>
@media screen and (max-width: 992px) {
  .margintop {
    margin-top: 50px;
  }
}
</style>
