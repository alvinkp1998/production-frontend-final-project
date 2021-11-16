<template>
  <div>
    <div class="box">
      <h3 class="center text-white display-4">
        <span class="font-bigger">Start learning from the best tutors</span>
        <nuxt-link to="/list-class"
          ><h5 class="text-white text-underline pt-3">
            Explore all classes
          </h5></nuxt-link
        >
      </h3>
    </div>
  </div>
</template>

<style scoped>
.box {
  border-radius: 30px;
  background-color: #923cb5;
  background-image: linear-gradient(147deg, #424142 0%, #6b3f75 74%);
  display: flex;
  height: 30vh;
}
.center {
  margin: auto;
}
.text-white {
  color: rgb(233, 224, 231) !important;
}
.text-underline {
  text-decoration: underline;
}
.font-bigger {
  font-size: 33px;
}
</style>
<script>
export default {
  auth: false
};
</script>
