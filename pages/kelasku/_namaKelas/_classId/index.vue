<template>
  <div>
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4 text-center">{{ forTitle }}</h1>
      </div>
    </div>

    <div class="container materi mb-4" v-for="item in listSesi" :key="item.id">
      <div class="row">
        <div
          class="box shadow-sm pt-3 pb-3 mb-3"
          data-toggle="collapse"
          :data-target="`#${item.id}`"
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
            <h4>Sesi {{ item.urutanSesi }} - {{ item.namaSesi }}</h4>
            <h5>{{ item.waktuMulai }}</h5>
          </div>

          <items-sesi-buttonEdit
            :id="item.id"
            :namaSesi="item.namaSesi"
            :urutanSesi="item.urutanSesi"
            :waktuMulai="item.waktuMulai"
            :waktuSelesai="item.waktuSelesai"
            v-if="$auth.loggedIn && $auth.user.status == 'admin'"
            @refreshData="GET_LIST_SESI"
          />
          <div v-if="$auth.loggedIn && $auth.user.status == 'admin'">
            <button
              class="btn btn-danger btn-sm pill mt-3 mr-4"
              @click="deleteSesi(item.id, item.namaSesi)"
            >
              Hapus
            </button>
          </div>
        </div>
        <div class="box-material collapse shadow " :id="item.id">
          <div class="row ml-3">
            <div
              class="col-md-5 kotak ml-3 mt-3 shadow-sm"
              v-for="material in item.Materials"
              :key="material.id"
            >
              <div class="row ml-2">
                <div class="col-md-4 pt-2 ">
                  <img
                    src="https://1.bp.blogspot.com/-LICFT7WO2vw/XipEPK6u2TI/AAAAAAAACW0/kj_E5a34EcQ0ofc929GlEfmS_XzXp-S4wCLcBGAsYHQ/s1600/index.png"
                    alt=""
                    width="80px"
                    height="80px"
                  />
                </div>
                <div class="col-md-8 pt-3">
                  <h4>{{ material.namaMateri }}</h4>
                  <p>{{ material.jenisMateri }}</p>
                </div>
              </div>
            </div>
          </div>
          <div>
            <button
              class="view-materi"
              @click="
                $router.push(
                  `/kelasku/${$route.params.namaKelas}/${$route.params.classId}/materi/${item.id}`
                )
              "
            >
              View Material
            </button>
          </div>
        </div>
      </div>
    </div>
    <items-sesi-buttonCreate
      @refreshData="GET_LIST_SESI"
      v-if="$auth.loggedIn && $auth.user.status == 'admin'"
    />
  </div>
</template>

<script>
import request from "../../../../mixins/request.vue";
export default {
  mixins: [request],
  data() {
    return {
      listSesi: [],
      muncul: false
    };
  },
  computed: {
    forTitle() {
      return this.$route.params.namaKelas.toUpperCase().replace(/-/g, " ");
    }
  },
  methods: {
    async GET_LIST_SESI() {
      const LIST_SESI = await this.requestGet(
        `/sesi/${this.$route.params.classId}`
      );
      console.log(LIST_SESI);
      this.listSesi = LIST_SESI;
    },
    toMaterial() {
      this.$router.push(
        `/kelasku/${$route.params.namaKelas}/${this.$route.params.classId}/${this.item.id}`
      );
    },

    async deleteSesi(id, nama) {
      const confirm = await this.confirm(`Menghapus Sesi ${nama}`);
      if (confirm.isConfirmed) {
        await this.requestDelete(`/sesi/${id}`);
        this.GET_LIST_SESI();
      }
    }
  },
  mounted() {
    this.GET_LIST_SESI();
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
.kotak {
  border-radius: 10px;
  cursor: pointer;
}
.kotak:hover {
  color: rgb(176, 102, 190);
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
.box-material {
  position: relative;
  width: 800px;
  height: 400px;
  /* background-color: blue; */
  border-radius: 30px;
}
.view-materi {
  position: absolute;
  border: none;
  bottom: 0;
  background-color: white;
  border-radius: 40px;
  transition: 0.3s ease-in-out;
  font-weight: bold;
  font-size: 20px;
  color: #ae9bfc;
  padding: 10px;

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
