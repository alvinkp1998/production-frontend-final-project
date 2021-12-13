<template>
  <div class="container">
    <div class="box-tutor">
      <h3 class="">Tutors & Fasilitator</h3>
      <hr />
      <div class="row">
        <div
          class="col-sm-4 col-md-3 col-6"
          v-for="teacher in listTeachers"
          :key="teacher.id"
        >
          <class-anggota
            :nama="teacher.nama"
            :roleId="teacher.Classes[0].JoinClasses.RoleId"
            :img="
              teacher.foto ||
                'https://w7.pngwing.com/pngs/81/570/png-transparent-profile-logo-computer-icons-user-user-blue-heroes-logo-thumbnail.png'
            "
          />
        </div>
      </div>
    </div>
    <div class="box-classmate mt-3">
      <h3 class="float-left">Classmates</h3>
      <h4 class="float-right">{{ listAnggota.length }} students</h4>
      <hr style="clear:both;" />
      <div class="row">
        <div
          class="col-sm-4 col-md-3 col-6"
          v-for="student in listStudents"
          :key="student.id"
        >
          <class-anggota
            :nama="student.nama"
            :roleId="student.Classes[0].JoinClasses.RoleId"
            :img="
              student.foto ||
                'https://w7.pngwing.com/pngs/81/570/png-transparent-profile-logo-computer-icons-user-user-blue-heroes-logo-thumbnail.png'
            "
          />
        </div>
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
  computed: {
    listStudents() {
      return this.listAnggota.filter(
        anggota => anggota.Classes[0].JoinClasses.RoleId === 3
      );
    },
    listTeachers() {
      return this.listAnggota.filter(
        anggota =>
          anggota.Classes[0].JoinClasses.RoleId === 1 ||
          anggota.Classes[0].JoinClasses.RoleId === 2
      );
    }
  },
  mounted() {
    this.GET_LIST_ANGGOTA();
  }
};
</script>

<style scoped>
.container {
  max-width: 1000px !important;
}
</style>
