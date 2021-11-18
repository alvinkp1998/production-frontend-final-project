<template>
  <div>
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4 text-center">{{ forTitle }}</h1>
      </div>
    </div>

    <div class="container materi">
      <div class="card shadow-sm">
        <div class="card-body">
          <div class="row">
            <div class="col-1 mr-4">
              <img src="/favicon.ico" width="40px" height="100%" alt="materi" />
            </div>
            <div class="col vertical-line">
              {{ $route.params }}
              <h4>{{ listSesi.namaSesi }} - Materi</h4>
              <h5>30 Agustus 2021</h5>
            </div>
            <div class="col-1 d-flex align-items-center ">
              <i
                class="fas fa-ellipsis-v"
                data-toggle="dropdown"
                style="font-size:1.4em"
              ></i>
              <div class="dropdown-menu">
                <a class="dropdown-item" href="#">Sunting</a>
                <a class="dropdown-item" href="#">Hapus</a>
              </div>
            </div>
          </div>
        </div>
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
      listSesi: [],
      listMateri: []
    };
  },
  computed: {
    forTitle() {
      return this.$route.params.classId.toUpperCase().replace(/-/g, " ");
    }
  },
  methods: {
    async GET_LIST_SESI() {
      const LIST_SESI = await this.requestGet("/sesi");
      console.log(LIST_SESI);
      // this.listSesi = LIST_SESI.data;
    },
    async GET_LIST_MATERI() {
      const LIST_MATERI = await this.requestGet("/materi");
      console.log(LIST_MATERI);
      // this.listClass = LIST_CLASS.data;
    }
  },
  mounted() {
    this.GET_LIST_SESI;
    this.GET_LIST_MATERI;
  }
};
</script>

<style scoped>
.jumbotron {
  color: #524e4e;
  height: 30vh;
  background: url("https://thumbs.dreamstime.com/b/banner-laptop-office-supply-yellow-background-copy-space-online-business-workspace-distance-education-e-learning-209978591.jpg");
  background-size: cover;
}

.container {
  display: flex;
  width: 40%;
  height: 100%;
}
.container.materi {
  width: 700px;
}
.display-4 {
  margin: auto;
}
.card {
  border-radius: 15px !important;
  background-color: rgb(245, 240, 240);
  width: 100%;
}
.vertical-line {
  margin-left: 20px;
  padding-left: 20px;
  border-left: 3px solid rgb(168, 167, 167);
}

.pointer {
  cursor: pointer;
}
</style>
