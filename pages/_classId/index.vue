<template>
  <div>
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4 text-center">{{ forTitle }}</h1>
      </div>
    </div>

    <div class="container materi mb-4" v-for="item in listSesi" :key="item.id">
      <div class="row shadow-sm">
        <div
          class="box pt-3 pb-3"
          :class="muncul ? 'background-purple shadow-sm' : 'background-white'"
          @click="muncul = !muncul"
        >
          <div class="col-1 mr-4">
            <img
              src="/images/materi.jpg"
              width="50px"
              height="100%"
              alt="materi"
            />
          </div>
          <div class="col">
            <h4>{{ item.namaSesi }}</h4>
            <h5>{{ item.waktuMulai }}</h5>
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
        <div class="box2" v-if="muncul">
          <nuxt-link :to="`/${$route.params.classId}/materi`"
            ><span class="view-materi">View Material</span></nuxt-link
          >
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
      listMateri: [],
      muncul: false
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
      const LIST_MATERI = await this.requestGet("/materi");
      console.log(LIST_SESI);
      console.log(LIST_MATERI);

      this.listSesi = LIST_SESI.data;
      this.listMateri = LIST_MATERI.data;
    },
    async GET_LIST_MATERI() {
      const LIST_MATERI = await this.requestGet("/materi");
      console.log(LIST_MATERI);

      this.listMateri = LIST_MATERI.data;
    },
    toMateri() {
      // this.$router.push(`/$routes.params.classId/materi`);
    }
  },
  mounted() {
    this.GET_LIST_SESI();
    // this.GET_LIST_MATERI();
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
  display: flex;
  justify-content: center;
  width: 700px;
}
.display-4 {
  margin: auto;
}
.background-purple {
  background-color: #cdc1ff;
  background-image: linear-gradient(316deg, #cdc1ff 0%, #e5d9f2 74%);
  border-bottom-left-radius: 0px;
  border-bottom-right-radius: 0px;
}
.background-white {
  background-color: white;
}
.box {
  /* background-color: rgb(237, 212, 243); */
  display: flex;
  justify-content: center;
  width: 800px;
  border-radius: 30px;
}
.box:hover {
  cursor: pointer;
  background-color: #cdc1ff;
  background-image: linear-gradient(316deg, #cdc1ff 0%, #e5d9f2 74%);
}
.box2 {
  position: relative;
  width: 800px;
  height: 300px;
  /* background-color: blue; */
  border-bottom-left-radius: 30px;
  border-bottom-right-radius: 30px;
}
.view-materi {
  position: absolute;
  font-weight: bold;
  font-size: 20px;
  color: #b3a3f1;
  padding: 10px;
  bottom: 0;
  margin-left: 15px;
  margin-bottom: 15px;
}
.view-materi:hover {
  cursor: pointer;
  background-color: #f6f4fd;
  padding: 10px;
}

.pointer {
  cursor: pointer;
}
</style>
