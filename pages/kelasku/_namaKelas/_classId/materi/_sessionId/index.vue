<template>
  <div>
    <div class="container">
      <h1 class="display-4 mb-3">Materi</h1>
    </div>
    <div>
      <div class="container garis">
        <div class="row">
          <div
            class="col-md-5 kotak ml-3 mt-3 shadow-sm"
            v-for="item in listMateri"
            :key="item.id"
          >
            <div class="row">
              <div class="col-md-4 pt-4 ">
                <img
                  src="https://1.bp.blogspot.com/-LICFT7WO2vw/XipEPK6u2TI/AAAAAAAACW0/kj_E5a34EcQ0ofc929GlEfmS_XzXp-S4wCLcBGAsYHQ/s1600/index.png"
                  alt=""
                  width="100px"
                  height="100px"
                />
              </div>
              <div class="col-md-6 pt-5">
                <h4>{{ item.namaMateri }}</h4>
                <p>{{ item.jenisMateri }}</p>
              </div>
              <div class="col-md-2">
                <div v-if="$auth.loggedIn && $auth.user.status == 'admin'">
                  <items-materi-buttonEdit
                    :id="item.id"
                    :namaMateri="item.namaMateri"
                    :jenisMateri="item.jenisMateri"
                    :file="item.file"
                    @refreshData="GET_LIST_MATERI"
                  />
                  <button
                    class="btn btn-danger btn-sm pill mt-3 mr-4"
                    @click="deleteMateri(item.id, item.namaMateri)"
                  >
                    Hapus
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <items-materi-buttonCreate
      @refreshData="GET_LIST_MATERI"
      v-if="$auth.loggedIn && $auth.user.status == 'admin'"
    />
  </div>
</template>

<script>
import request from "../../../../../../mixins/request.vue";
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
    },
    async deleteMateri(id, nama) {
      const confirm = await this.confirm(`Menghapus Materi ${nama}`);
      if (confirm.isConfirmed) {
        await this.requestDelete(`/materi/${id}`);
        this.GET_LIST_MATERI();
      }
    }
  },
  mounted() {
    this.GET_LIST_MATERI();
  }
};
</script>

<style scoped>
.kotak {
  border-radius: 10px;
  height: 150px;
  cursor: pointer;
}
.kotak:hover {
  color: rgb(176, 102, 190);
}

.garis {
  border-top: 2px solid rgb(221, 194, 223);
}
.jumbotron {
  border-radius: 20px;
  color: #524e4e;
  /* background-color: white; */
  background-color: #463399 !important;
  background-image: linear-gradient(316deg, #cdc1ff 0%, #e5d9f2 74%) !important;
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
