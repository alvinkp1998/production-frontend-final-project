<template>
  <div>
    <div class="card shadow-lg">
      <div class="text-center">
        <img
          class="card-img-top gambar "
          :src="img"
          alt="Card image cap"
          width="100%"
          height="170px"
        />
      </div>

      <div class="card-body">
        <h5 class="card-text text text-center">{{ name }}</h5>
      </div>
      <kelasku-modal :id="id" :img="img" :name="name" :desc="desc" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    id: { type: Number },
    name: { type: String },
    desc: { type: String },
    img: { type: String }
  }
};
</script>

<style scoped>
.card {
  max-width: 400px;
  min-width: 150px;
  padding: 1.2em;
  background-color: white;
}

.gambar {
  max-width: 300px;
}

/* // Small devices (landscape phones, 576px and up) */
@media (min-width: 576px) {
  .text {
    font-size: 20px;
  }
}

/* // Medium devices (tablets, 768px and up) */
@media (min-width: 768px) {
  .text {
    font-size: 15px;
  }
}

/* // Large devices (desktops, 992px and up) */
@media (min-width: 992px) {
  .text {
    font-size: 14px;
  }
}

/* // Extra large devices (large desktops, 1200px and up) */
@media (min-width: 1200px) {
  .text {
    font-size: 17px;
  }
}
</style>
