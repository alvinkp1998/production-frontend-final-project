<template>
  <div>
    <div class="row ">
      <div
        class="col-lg-3 col-md-6 margintop mb-5"
        v-for="item in listClass"
        :key="item.id"
      >
        <kelasku-item
          @refreshData="GET_LIST_CLASS"
          :id="item.id"
          :kode="item.Class.kodeKelas"
          :nama="item.Class.namaKelas"
          :deskripsi="item.Class.deskripsiKelas"
          :tanggalMulai="item.Class.tanggalMulai"
          :tanggalSelesai="item.Class.tanggalSelesai"
          :foto="item.Class.fotoKelas"
        />
      </div>
    </div>
  </div>
</template>

<script>
import request from "../../mixins/request.vue";
export default {
  mixins: [request],
  data() {
    return {
      listClass: []
    };
  },
  methods: {
    async GET_LIST_CLASS() {
      const LIST_CLASS = await this.requestGet("/join");
      console.log(LIST_CLASS);
      this.listClass = LIST_CLASS.data;
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
