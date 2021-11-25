<template>
  <div class="container">
    <h3 class="float-left">Anggota</h3>
    <h4 class="float-right">{{ listAnggota.length }} anggota</h4>
    <hr style="clear:both;" />
    <div class="row">
      <div
        class="col-sm-4 col-md-3 col-6"
        v-for="item in listAnggota"
        :key="item.id"
      >
        <class-anggota
          :nama="item.nama"
          :roleId="item.Classes[0].JoinClasses.RoleId"
        />
      </div>
    </div>
  </div>
</template>

<script>
import request from "../../../../../mixins/request.vue";
export default {
  mixins: [request],
  data() {
    return {
      listAnggota: []
    };
  },
  methods: {
    async GET_LIST_ANGGOTA() {
      const LIST_ANGGOTA = await this.requestGet(
        `/join/${this.$route.params.classId}`
      );
      console.log(LIST_ANGGOTA);
      this.listAnggota = LIST_ANGGOTA.data;
    }
  },
  mounted() {
    this.GET_LIST_ANGGOTA();
  }
};
</script>
