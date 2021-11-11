<template>
  <div>
    <div class="row ">
      <div
        class="col-lg-3 col-md-6 margintop"
        v-for="item in listClass"
        :key="item.id"
      >
        <kelasku-item
          :id="item.id"
          :name="item.name"
          :desc="item.desc"
          :img="item.img"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      listClass: [
        {
          id: 1,
          name: "Mastery Laravel",
          desc:
            "Ini kelas Laravel Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat",
          img:
            "https://cms-assets.tutsplus.com/uploads/users/769/posts/25334/preview_image/get-started-with-laravel-6-400x277.png"
        },
        {
          id: 2,
          name: "Mastery Node js",
          desc: "Ini kelas Node.js",
          img:
            "https://static.cdn-cdpl.com/source/998b78e349061b4971c0a2b0e8d6be41/nodejs-frameworks.png"
        },
        {
          id: 3,
          name: "Mastery Vue js",
          desc: "Ini kelas Vue.js",
          img: "https://miro.medium.com/max/1400/1*wFL3csJ96lQpY0IVT9SE3w.jpeg"
        },
        {
          id: 4,
          name: "Mastery Angular js",
          desc: "Ini kelas Angular.js",
          img:
            "http://redaksi.pens.ac.id/wp-content/uploads/2021/01/Reasons-to-Choose-AngularJS.png"
        }
      ]
    };
  }
};
</script>

<style scoped>
@media screen and (max-width: 992px) {
  .margintop {
    margin-top: 50px;
  }
}
</style>
