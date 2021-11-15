<template>
  <div>
    <nav class="sidebar sidebar-offcanvas" id="sidebar">
      <ul class="nav">
        <li class="nav-item nav-profile" v-if="$auth.user">
          <a href="#" class="nav-link">
            <div class="nav-profile-image">
              <img src="images/fotoku.jpg" alt="profile" />
              <span class="login-status online"></span>
            </div>
            <div class="nav-profile-text d-flex flex-column">
              <span class="font-weight-bold mb-2">{{ $auth.user.nama }}</span>
              <span class="text-secondary text-small">Student</span>
            </div>
            <i
              class="mdi mdi-bookmark-check text-success nav-profile-badge"
            ></i>
          </a>
        </li>
        <li class="nav-item" v-for="(menu, i) in listSidebar" :key="i">
          <nuxt-link class="nav-link" :to="menu.to">
            <span class="menu-title pl-2">{{ menu.name }}</span>
            <i :class="menu.icon"></i>
          </nuxt-link>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  data() {
    return {
      listSidebar: [
        {
          name: "Home",
          icon: "fas fa-home menu-icon",
          to: "/"
        },
        {
          name: "Semua Kelas",
          icon: "fas fa-chalkboard menu-icon",
          to: "/list-class"
        },
        {
          name: "Kelasku",
          icon: "fas fa-book-open menu-icon",
          to: "/kelasku"
        },
        {
          name: "Presensi",
          icon: "far fa-check-square menu-icon",
          to: "/list-class"
        }
      ]
    };
  }
};
</script>
