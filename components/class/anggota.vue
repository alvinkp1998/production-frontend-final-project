<template>
  <div>
    <div class="card">
      <img
        :srcset="img"
        class="card-img-top rounded-circle"
        width="200px"
        height="200px"
      />
      <div class="row px-2">
        <div class="col">
          <h5 class="p-0 pt-2 m-0">{{ nama }}</h5>
          <p v-if="roleId === 3" class="">-Student-</p>
          <p v-if="roleId === 2">-Fasilitator-</p>
          <p v-if="roleId === 1">-Tutor-</p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    nama: String,
    // role: String,
    img: {
      type: String,
      default:
        "https://w7.pngwing.com/pngs/81/570/png-transparent-profile-logo-computer-icons-user-user-blue-heroes-logo-thumbnail.png"
    },
    roleId: Number
  }
};
</script>
