<template>
  <div>
    <nav
      class="navbar default-layout-navbar col-lg-12 col-12 p-0 fixed-top d-flex flex-row"
    >
      <div
        class="text-center navbar-brand-wrapper d-flex align-items-center justify-content-center"
      >
        <nuxt-link class="navbar-brand brand-logo" to="/"
          ><img src="/images/fs.png" alt="logo"
        /></nuxt-link>
        <nuxt-link class="navbar-brand brand-logo-mini" to="/"
          ><img src="/images/fs-mini.png" alt="logo"
        /></nuxt-link>
      </div>
      <div class="navbar-menu-wrapper d-flex align-items-stretch bg">
        <ul
          v-if="$route.params.namaKelas"
          class="navbar-nav text-black"
          style="margin-left:300px"
        >
          <li class="nav-item border-right border-left ">
            <nuxt-link
              class="nav-link"
              :to="
                `/kelasku/${$route.params.namaKelas}/${$route.params.classId}`
              "
              >Kelas</nuxt-link
            >
          </li>
          <!-- <li class="nav-item border-right">
            <nuxt-link
              class="nav-link"
              :to="
                `/kelasku/${$route.params.classId}/${$route.params.classId}/jadwal`
              "
              >Sesi</nuxt-link
            >
          </li> -->
          <li class="nav-item border-right">
            <nuxt-link
              class="nav-link"
              :to="
                `/kelasku/${$route.params.namaKelas}/${$route.params.classId}/anggota`
              "
              >Anggota</nuxt-link
            >
          </li>
        </ul>
        <ul class="navbar-nav navbar-nav-right">
          <li class="nav-item nav-profile dropdown" v-if="$auth.user">
            <a
              class="nav-link dropdown-toggle"
              id="profileDropdown"
              href="#"
              data-toggle="dropdown"
              aria-expanded="false"
            >
              <div class="nav-profile-img">
                <img
                  :src="
                    $auth.user.foto ||
                      'https://w7.pngwing.com/pngs/81/570/png-transparent-profile-logo-computer-icons-user-user-blue-heroes-logo-thumbnail.png'
                  "
                  alt="image"
                />
                <span class="availability-status online"></span>
              </div>
              <div class="nav-profile-text">
                <p class="mb-1 text-black">{{ $auth.user.nama }}</p>
              </div>
            </a>
            <div
              class="dropdown-menu navbar-dropdown"
              aria-labelledby="profileDropdown"
            >
              <nuxt-link to="/profile" class="dropdown-item">
                <i class="mdi mdi-cached mr-2 text-success"></i>
                My Profile
              </nuxt-link>
              <div class="dropdown-divider"></div>
              <a class="dropdown-item" href="#" @click="logout">
                <i class="mdi mdi-logout mr-2 text-primary"></i>
                Signout
              </a>
            </div>
          </li>
          <li class="nav-item d-none d-lg-block full-screen-link">
            <a class="nav-link">
              <i class="mdi mdi-fullscreen" id="fullscreen-button"></i>
            </a>
          </li>
          <li class="nav-item" v-if="!$auth.user">
            <button class="btn btn-primary btn-sm" @click="toLogin">
              Login
            </button>
          </li>
          <li class="nav-item ml-2" v-if="!$auth.user" s>
            <button class="btn btn-primary btn-sm" @click="toRegister">
              Sign up
            </button>
          </li>
          <li class="nav-item dropdown" v-if="$auth.user">
            <a
              class="nav-link count-indicator dropdown-toggle"
              id="messageDropdown"
              href="#"
              data-toggle="dropdown"
              aria-expanded="false"
            >
              <i class="mdi mdi-email-outline"></i>
              <span class="count-symbol bg-warning"></span>
            </a>
            <div
              class="dropdown-menu dropdown-menu-right navbar-dropdown preview-list"
              aria-labelledby="messageDropdown"
            >
              <h6 class="p-3 mb-0">Messages</h6>
              <div class="dropdown-divider"></div>
              <a class="dropdown-item preview-item">
                <div class="preview-thumbnail">
                  <img
                    src="/images/faces/face4.jpg"
                    alt="image"
                    class="profile-pic"
                  />
                </div>
                <div
                  class="preview-item-content d-flex align-items-start flex-column justify-content-center"
                >
                  <h6 class="preview-subject ellipsis mb-1 font-weight-normal">
                    Mark send you a message
                  </h6>
                  <p class="text-gray mb-0">
                    1 Minutes ago
                  </p>
                </div>
              </a>
              <div class="dropdown-divider"></div>
              <a class="dropdown-item preview-item">
                <div class="preview-thumbnail">
                  <img
                    src="/images/faces/face2.jpg"
                    alt="image"
                    class="profile-pic"
                  />
                </div>
                <div
                  class="preview-item-content d-flex align-items-start flex-column justify-content-center"
                >
                  <h6 class="preview-subject ellipsis mb-1 font-weight-normal">
                    Cregh send you a message
                  </h6>
                  <p class="text-gray mb-0">
                    15 Minutes ago
                  </p>
                </div>
              </a>
              <div class="dropdown-divider"></div>
              <a class="dropdown-item preview-item">
                <div class="preview-thumbnail">
                  <img
                    src="/images/faces/face3.jpg"
                    alt="image"
                    class="profile-pic"
                  />
                </div>
                <div
                  class="preview-item-content d-flex align-items-start flex-column justify-content-center"
                >
                  <h6 class="preview-subject ellipsis mb-1 font-weight-normal">
                    Profile picture updated
                  </h6>
                  <p class="text-gray mb-0">
                    18 Minutes ago
                  </p>
                </div>
              </a>
              <div class="dropdown-divider"></div>
              <h6 class="p-3 mb-0 text-center">4 new messages</h6>
            </div>
          </li>
          <li class="nav-item dropdown" v-if="$auth.user">
            <a
              class="nav-link count-indicator dropdown-toggle"
              id="notificationDropdown"
              href="#"
              data-toggle="dropdown"
            >
              <i class="mdi mdi-bell-outline"></i>
              <span class="count-symbol bg-danger"></span>
            </a>
            <div
              class="dropdown-menu dropdown-menu-right navbar-dropdown preview-list"
              aria-labelledby="notificationDropdown"
            >
              <h6 class="p-3 mb-0">Notifications</h6>
              <div class="dropdown-divider"></div>
              <a class="dropdown-item preview-item">
                <div class="preview-thumbnail">
                  <div class="preview-icon bg-success">
                    <i class="mdi mdi-calendar"></i>
                  </div>
                </div>
                <div
                  class="preview-item-content d-flex align-items-start flex-column justify-content-center"
                >
                  <h6 class="preview-subject font-weight-normal mb-1">
                    Event today
                  </h6>
                  <p class="text-gray ellipsis mb-0">
                    Just a reminder that you have an event today
                  </p>
                </div>
              </a>
              <div class="dropdown-divider"></div>
              <a class="dropdown-item preview-item">
                <div class="preview-thumbnail">
                  <div class="preview-icon bg-warning">
                    <i class="mdi mdi-settings"></i>
                  </div>
                </div>
                <div
                  class="preview-item-content d-flex align-items-start flex-column justify-content-center"
                >
                  <h6 class="preview-subject font-weight-normal mb-1">
                    Settings
                  </h6>
                  <p class="text-gray ellipsis mb-0">
                    Update dashboard
                  </p>
                </div>
              </a>
              <div class="dropdown-divider"></div>
              <a class="dropdown-item preview-item">
                <div class="preview-thumbnail">
                  <div class="preview-icon bg-info">
                    <i class="mdi mdi-link-variant"></i>
                  </div>
                </div>
                <div
                  class="preview-item-content d-flex align-items-start flex-column justify-content-center"
                >
                  <h6 class="preview-subject font-weight-normal mb-1">
                    Launch Admin
                  </h6>
                  <p class="text-gray ellipsis mb-0">
                    New admin wow!
                  </p>
                </div>
              </a>
              <div class="dropdown-divider"></div>
              <h6 class="p-3 mb-0 text-center">See all notifications</h6>
            </div>
          </li>
          <li
            class="nav-item nav-logout d-none d-lg-block"
            v-if="$auth.user"
            @click="logout"
          >
            <a class="nav-link" href="#">
              <i class="mdi mdi-power"></i>
            </a>
          </li>
        </ul>
      </div>
    </nav>
  </div>
</template>

<style scoped>
.text-black {
  color: black;
}
</style>

<script>
export default {
  methods: {
    async logout() {
      await this.$auth.logout();
      this.$router.push("/login");
    },
    toLogin() {
      this.$router.push("/login");
    },
    toRegister() {
      this.$router.push("/register");
    }
  }
};
</script>
