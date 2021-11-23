<template>
  <div class="container">
    <h3>Teachers</h3>
    <hr />
    <div class="row">
      <div
        class="col-sm-4 col-md-3 col-6"
        v-for="item in listTeachers"
        :key="item.id"
      >
        <class-anggota :nama="item.nama" />
      </div>
    </div>

    <h3 class="float-left">Classmates</h3>
    <h4 class="float-right">{{ listStudents.length }} students</h4>
    <hr style="clear:both;" />
    <div class="row">
      <div
        class="col-sm-4 col-md-3 col-6"
        v-for="item in listStudents"
        :key="item.id"
      >
        <class-anggota :nama="item.nama" />
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
      listStudents: [],
      listTeachers: []
    };
  },
  methods: {
    async GET_LIST_ANGGOTA() {
      const LIST_ANGGOTA = await this.requestGet(
        `/join/${this.$route.params.classId}`
      );
      console.log(LIST_ANGGOTA);
      this.listStudents = LIST_ANGGOTA.data;
    }
  },
  mounted() {
    this.GET_LIST_ANGGOTA();
  }
};
</script>
