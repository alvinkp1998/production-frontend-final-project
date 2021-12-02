<template>
  <div>
    <nav class="sidebar sidebar-offcanvas" id="sidebar">
      <ul class="nav">
        <li class="nav-item nav-profile" v-if="$auth.user">
          <a href="#" class="nav-link">
            <div class="nav-profile-image">
              <img
                src="https://w7.pngwing.com/pngs/81/570/png-transparent-profile-logo-computer-icons-user-user-blue-heroes-logo-thumbnail.png"
                alt="profile"
              />
              <span class="login-status online"></span>
            </div>
            <div class="nav-profile-text d-flex flex-column">
              <span class="font-weight-bold mb-2">{{ $auth.user.nama }}</span>
              <span
                class="text-small text-status font-weight-bold text-capitalize "
                >- {{ $auth.user.status }} -</span
              >
            </div>
          </a>
        </li>
        <!-- Tampilan sidebar dari user profile  -->
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
          name: "My Profile",
          icon: "fas fa-user-tag menu-icon",
          to: "/profile"
        }
      ]
    };
  }
};
</script>

<style scoped>
.text-status {
  color: rgba(99, 103, 112, 0.993);
}
</style>
