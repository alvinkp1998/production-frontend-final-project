<template>
  <div>
    <div class="container">
      <h1 class="display-4 mb-3">Sesi {{ $route.params.sessionId }}</h1>
    </div>
    <div v-for="item in listMateri" :key="item.id">
      <div class=" jumbotron-fluid mt-3 mb-5">
        <div class="container materi mb-5">
          <div class="row shadow-sm">
            <div class="box pt-3 pb-3">
              <div class="col-1 mr-4">
                <img
                  src="/images/materi.jpg"
                  width="50px"
                  height="100%"
                  alt="materi"
                />
              </div>
              <div class="col">
                <h4>{{ item.namaMateri }}</h4>
                <h5>{{ item.jenisMateri }}</h5>
              </div>
            </div>
          </div>
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
      listMateri: []
    };
  },
  methods: {
    async GET_LIST_MATERI() {
      const LIST_MATERI = await this.requestGet(
        `/materi/${this.$route.params.sessionId}`
      );
      console.log(LIST_MATERI);
      this.listMateri = LIST_MATERI;
    }
  },
  mounted() {
    this.GET_LIST_MATERI();
  }
};
</script>

<style scoped>
.jumbotron {
  border-radius: 20px;
  color: #524e4e;
  /* background-color: white; */
  background-color: #463399 !important;
  background-image: linear-gradient(316deg, #cdc1ff 0%, #e5d9f2 74%) !important;
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
