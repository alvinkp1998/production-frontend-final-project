<template>
  <div>
    <span @click="$router.go(-1)" style="cursor:pointer">
      <h5 class="d-inline">
        <i class="fas fa-arrow-left mr-3 pointer"></i>
        Back
      </h5>
    </span>

    <hr />
    <div class="card">
      <div class="container mt-2">
        <form @submit.prevent="submit">
          <div class="row my-3">
            <div class="col-md-3 d-flex align-items-center">
              <label class="text-capitalize h6">Nama Jadwal</label>
            </div>
            <div class="col-md-9">
              <input type="text" v-model="data" class="form-control" />
            </div>
          </div>
          <div class="row my-3">
            <div class="col-md-3 d-flex align-items-center">
              <label class="text-capitalize h6">Waktu Mulai</label>
            </div>
            <div class="col-md-9">
              <input type="date" v-model="data" class="form-control" />
            </div>
          </div>
          <div class="row my-3">
            <div class="col-md-3 d-flex align-items-center">
              <label class="text-capitalize h6">Waktu Selesai </label>
            </div>
            <div class="col-md-9">
              <input type="date" v-model="data" class="form-control" />
            </div>
          </div>
          <div class="text-right mt-4">
            <button
              class="btn btn-secondary mr-3"
              @click="$router.go(-1)"
              type="button"
            >
              Batal
            </button>
            <button class="btn btn-primary" type="submit">Tambah</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  padding-top: 20px;
  padding-bottom: 20px;
  border-radius: 20px;
  background-color: rgb(250, 239, 255);
}
</style>
