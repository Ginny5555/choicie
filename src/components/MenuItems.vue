<template>
  <div class="hello">
    <div
      v-if="isHelloGreen"
      class="user"
      :style="{ backgroundColor: isUserBackgroundBlue ? '#3B2186' : 'transparent' }"
    >
      <div class="custom-container">
        <nav class="navbar navbar-expand-lg navbar-light w-100">
          <div class="row d-flex justify-content-between w-100">
            <div class="col-7 p-0">
              <button
                class="navbar-toggler"
                type="button"
                data-toggle="collapse"
                data-target="#navbarNavDropdown"
                aria-controls="navbarNavDropdown"
                aria-expanded="false"
                aria-label="Toggle navigation"
                @click="toggleUserBackground"
              >
                <span class="navbar-toggler-icon" v-if="isUserBackgroundBlue"></span>
                <span class="navbar-toggler-icon black" v-if="!isUserBackgroundBlue"></span>
              </button>
              <img
                class="logo yel d-sm-none d-none d-lg-block"
                src="../assets/logo2.svg"
                alt
                v-if="!shouldShowLogo && !isUserBackgroundBlue"
              />
              <img class="logo yel" src="../assets/logo2.svg" alt v-if="isUserBackgroundBlue" />
              <img
                class="logo d-lg-none"
                src="../assets/logo.svg"
                v-if="!isUserBackgroundBlue && !shouldShowLogo "
                alt
              />
            </div>
            <div class="col-4 user-btn p-0 d-flex justify-content-end">
              <div class="d-flex flex-row">
                <button
                  class="owner-os__white android d-lg-none d-md-block d-sm-block"
                  v-if="shouldShowButton"
                ></button>
                <button
                  class="owner-os__white ios d-lg-none d-md-block d-sm-block"
                  v-if="shouldShowButton"
                ></button>
              </div>
              <div class="d-flex flex-row">
                <button
                  class="user-os android d-lg-none d-md-block d-sm-block"
                  v-if="!shouldShowButton"
                ></button>
                <button
                  class="user-os ios d-lg-none d-md-block d-sm-block"
                  v-if="!shouldShowButton"
                ></button>
              </div>
            </div>
          </div>
          <div class="row owner-bar m-0">
            <div class="collapse navbar-collapse" id="navbarNavDropdown">
              <ul
                class="navbar-nav d-flex w-100 align-items-center justify-content-lg-between justify-content-center align-items-center"
              >
                <li class="nav-item">
                  <a @click="handleHelloClick">Home</a>
                </li>
                <li class="nav-item">
                  <a @click="handleAboutClick">About</a>
                </li>
                <li class="nav-item">
                  <a href="#/api">Client</a>
                </li>
                <li class="nav-item d-lg-block d-none">
                  <a href="#">How to use</a>
                </li>
                <li class="nav-item">
                  <a href="#">Contact</a>
                </li>
              </ul>
            </div>
          </div>
          <div class="d-flex flex-row">
            <button class="user-os android d-none d-lg-block d-md-none d-sm-none">
              <span>Android</span>
            </button>
            <button class="user-os ios d-lg-block d-none d-md-none d-sm-none">
              <span>iOS</span>
            </button>
          </div>
        </nav>
      </div>
    </div>

    <div
      v-if="isHelloRed"
      class="owner"
      :style="{ backgroundColor: isUserBackgroundBlue ? '#3B2186' : 'transparent' }"
    >
      <div class="custom-container">
        <nav class="navbar navbar-expand-lg navbar-light w-100 d-flex justify-content-between">
          <div>
            <button
              class="navbar-toggler"
              type="button"
              data-toggle="collapse"
              data-target="#navbarNavDropdown"
              aria-controls="navbarNavDropdown"
              aria-expanded="false"
              aria-label="Toggle navigation"
              @click="toggleUserBackground"
            >
              <span class="navbar-toggler-icon" v-if="isUserBackgroundBlue"></span>
              <span class="navbar-toggler-icon black" v-if="!isUserBackgroundBlue"></span>
            </button>
            <img class="logo" src="../assets/logo.svg" alt v-if="!shouldShowButton" />
            <img class="logo" src="../assets/logo2.svg" alt v-if="shouldShowButton" />
          </div>
          <div class="d-flex flex-row">
            <button
              class="owner-os android d-lg-none d-md-block d-sm-block"
              v-if="!shouldShowButton"
            ></button>
            <div class="d-flex flex-row">
              <button
                class="owner-os__white android d-lg-none d-md-block d-sm-block"
                v-if="shouldShowButton"
              ></button>
              <button
                class="owner-os__white ios d-lg-none d-md-block d-sm-block"
                v-if="shouldShowButton"
              ></button>
            </div>
            <button class="owner-os ios d-lg-none d-md-block d-sm-block" v-if="!shouldShowButton"></button>
          </div>
          <div class="row owner-bar">
            <div class="collapse navbar-collapse" id="navbarNavDropdown">
              <ul
                class="navbar-nav col-12 p-0 owner-bar__items d-flex w-100 align-items-center justify-content-center"
              >
                <li class="nav-item">
                  <a @click=" handleHelloClick">Home</a>
                </li>
                <li class="nav-item">
                  <a @click=" handleAboutClick">About</a>
                </li>
                <li class="nav-item">
                  <a href="#/api">Client</a>
                </li>
                <li class="nav-item">
                  <a>Contact</a>
                </li>
              </ul>
            </div>
            <div class="col-md-12 col-sm-6 p-0 d-flex w-100 justify-content-between">
              <button
                class="owner-os android d-none d-lg-block d-md-none d-sm-none"
                v-if="!shouldShowButton"
              >
                <span>Android</span>
              </button>
              <button
                class="owner-os ios d-none d-lg-block d-md-none d-sm-none"
                v-if="!shouldShowButton"
              >
                <span>iOS Store</span>
              </button>
            </div>
          </div>
        </nav>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MenuItems",
  props: {
    msg: String
  },
  data() {
    return {
      isHelloRed: false,
      isHelloGreen: true,
      isUserBackgroundBlue: false
    };
  },
  mounted() {
    this.updateActiveSection();
  },
  watch: {
    $route() {
      this.updateActiveSection();
    }
  },
  computed: {
    iconStyle() {
      return this.isUserBackgroundBlue
        ? "url('../assets/menu1.svg')!important"
        : "url('../assets/menu2.svg')!important";
    }
  },
  methods: {
    handleHelloClick() {
      if (this.$route.path !== "/") {
        this.$router.push("/");
      }
    },
    handleAboutClick() {
      if (this.$route.path !== "/about") {
        this.$router.push("/about");
      }
    },
    updateActiveSection() {
      this.isHelloGreen = this.$route.path === "/";
      this.isHelloRed = this.$route.path === "/about";
    },
    toggleUserBackground() {
      if (window.innerWidth < 994) {
        this.isUserBackgroundBlue = !this.isUserBackgroundBlue;
        this.shouldShowButton = this.isUserBackgroundBlue;
      }
      if (window.innerWidth > 990) {
        this.shouldShowLogo = !this.shouldShowLogo;
      }
    }
  }
};
</script>

<style lang="scss">
@import "../assets/styles.scss";
ul {
  margin-block-start: 0;
  margin-block-end: 0;
}
.navbar {
  padding: 0 !important;
}
span.navbar-toggler-icon {
  width: 16px;
}

.nav-item a {
  background: none;
  border: none;
}
button.navbar-toggler {
  border: none;
}
.user {
  display: block;
  padding-top: 40px;
  & .navbar-light .navbar-toggler-icon {
    background-image: url("../assets/menu1.svg") !important;
  }
  & .navbar-light .navbar-toggler-icon.black {
    background-image: url("../assets/menu2.svg") !important;
  }
  &-os {
    display: inline-flex;
    padding: 14px 24px;
    justify-content: center;
    align-items: center;
    gap: 10px;
    border: none;
    width: 139px;
    border-radius: 50px;
    &__white {
      border-radius: 50%;
      width: 44px;
      height: 44px;
      padding: 14px 24px;
      border: none;
      background-size: cover;
      background-position: center;
      background-size: 16px;
      background-repeat: no-repeat;
      background: $white;
      &:hover {
        background-color: $text-grey;
      }
      &.ios {
        background-image: url("../assets/ios-black.svg");
      }
      &.android {
        background-image: url("../assets/android-black.svg");
        margin-right: 16px;
      }
    }
    &.android {
      color: $white;
      background: $drpurple-nav;

      padding: 14px 24px;
      background-image: url("../assets/android-white.svg");
      background-size: cover;
      background-position: left;
      background-size: 16px;
      background-repeat: no-repeat;

      font-size: 16px;
      font-weight: 600;
      line-height: 24px;
      margin-right: 16px;
      background-position: 24px 17px;
      text-align: right;
      &:hover {
        background-color: $purple-focus;
      }
      &:focus {
        background-color: $purple-focus;
      }
      &:disabled {
        background-color: $purple-disabled;
        color: $drpurple-nav;
      }
    }
    &.ios {
      width: 147px;
      color: $drpurple-nav;
      background: $brand-yellow;
      text-align: center;
      font-size: 16px;
      font-weight: 600;
      line-height: 24px;
      background-position: 39px 15px;

      padding: 14px 24px;
      background-image: url("../assets/ios1-dark.svg");
      background-size: cover;

      background-size: 16px;
      background-repeat: no-repeat;
      & span {
        margin-left: 19px;
      }
      &:hover {
        background-color: $yellow-focus;
      }
      &:focus {
        background-color: $yellow-focus;
      }
      &:disabled {
        color: $brand-yellow;
        background: $yellow-disabled;
      }
    }
  }
  & .navbar-nav a {
    font-size: 16px;
    color: $white;
    font-style: normal;
    font-weight: 600;
    line-height: 20px;
    margin-right: 50px;
    width: fit-content;
    text-wrap: nowrap;

    &::after {
      content: "";
      position: absolute;
      left: 50%;
      bottom: -13px;
      transform: translateX(-50%);
      width: 16px;
      height: 3px;
      background-color: $brand-yellow;
      opacity: 0;
      transition: opacity 0.3s ease;
    }

    &:hover::after {
      opacity: 1;
    }
  }
}

.owner {
  padding-top: 40px;
  & .navbar-nav {
    margin-bottom: -28px;
    margin-left: -4px;
    z-index: 1;
  }
  display: block;
  &-bar {
    width: 669px;
  }
  .navbar-nav a {
    font-size: 16px;
    color: $white;
    font-style: normal;
    font-weight: 600;
    line-height: 20px;
    margin-right: 50px;
    width: fit-content;
    text-wrap: nowrap;
  }
  & button {
    border-radius: 50px;
  }
  &-os {
    border-radius: 50px;
    padding: 14px 24px;
    justify-content: center;
    align-items: center;
    gap: 10px;
    border: none;
    &__white {
      border-radius: 50%;
      width: 44px;
      height: 44px;
      padding: 14px 24px;
      border: none;
      background-size: cover;
      background-position: center;
      background-size: 16px;
      background-repeat: no-repeat;
      background-color: $white;
      &:hover {
        background-color: $text-grey;
      }

      &.ios {
        background-image: url("../assets/ios-black.svg");
      }
      &.android {
        background-image: url("../assets/android-black.svg");
        margin-right: 16px !important;
      }
    }
    &.ios {
      background: $brand-yellow;
      color: $white;
      width: 147px;
      padding: 14px 24px;
      text-align: right;
      background-image: url("../assets/ios-white.svg");
      background-size: cover;
      background-position: left;
      background-size: 16px;
      background-repeat: no-repeat;
      background-position: 25px 17px;
      &:hover {
        background-color: $yellow-focus;
      }
      &:focus {
        background-color: $yellow-focus;
      }
      &:disabled {
        color: $brand-yellow;
        background: $yellow-disabled;
      }
    }
    &.android {
      background: $drpurple-nav;
      color: $white;
      text-align: right;
      width: 139px;
      padding: 14px 24px;
      background-image: url("../assets/android-white.svg");
      background-size: cover;
      background-position: 25px 17px;
      background-size: 16px;
      background-repeat: no-repeat;
      &:hover {
        background-color: $purple-focus;
      }
      &:focus {
        background-color: $purple-focus;
      }
      &:disabled {
        background-color: $purple-disabled;
        color: $drpurple-nav;
      }
    }
  }
  & .navbar-nav .nav-item a {
    color: $about-nav;
  }
  & .navbar-nav {
    display: flex;
    justify-content: center;
  }

  & .nav-item:nth-child(1) a {
    margin-left: 13px;
    margin-right: 50px;
  }

  & .nav-item:nth-child(2) a {
    margin-right: 50px;
  }

  & .nav-item:nth-child(3) a {
    margin-right: 50px;
  }

  & .nav-item:nth-child(4) a {
    margin-right: 13px;
  }
  & .navbar-light .navbar-toggler-icon {
    background-image: url("../assets/menu1.svg") !important;
  }
  & .navbar-light .navbar-toggler-icon.black {
    background-image: url("../assets/menu2.svg") !important;
  }
}
.navbar-nav .nav-item a {
  font-size: 16px;
  color: $white;
  font-style: normal;
  font-weight: 600;
  line-height: 20px;
  border: none;
  position: relative;
}

.logo {
  width: 182.183px;
  height: 52px;
  margin-right: 0;
}
@media screen and (min-width: 320px) and (max-width: 767px) {
  .logo {
    width: 120.6px;
  }
  .user {
    position: absolute;
    z-index: 2;
    padding-top: 8px;
    width: 100%;
    &-btn {
      margin-right: -19px;
    }
    &-os {
      &.ios {
        color: $drpurple-nav;
        background: $brand-yellow;
        width: 44px;
        height: 44px;
        padding: 14px 24px;
        background-image: url("../assets/ios-white.svg") !important;
        background-size: cover;
        background-position: center;
        background-size: 16px;
        background-repeat: no-repeat;
        &:hover {
          background-color: $yellow-focus;
        }
        &:focus {
          background-color: $yellow-focus;
        }
        &:disabled {
          color: $brand-yellow;
          background: $yellow-disabled;
        }
      }
      &.android {
        width: 44px;
        height: 44px;
        padding: 14px 24px;
        background-image: url("../assets/android-white.svg") !important;
        background-size: cover;
        background-position: center;
        background-size: 16px;
        background-repeat: no-repeat;
        margin-right: 16px;
      }
    }
    & .navbar-nav {
      margin-bottom: 0 !important;
          margin-top: 29px;
      & li {
        width: 100%;
        padding: 16px 0;
        border-bottom: 1px solid $line-nav;
        display: flex;
        justify-content: center;
        & a::after {
          display: none;
        }
        &:hover {
          background-color: $purple-focus;
        }

        &.nav-item a {
          color: $white;
          margin:0;
        }
      }
    }
  }
  .owner {
    position: absolute;
    z-index: 2;
    width: 100%;
    padding-top: 8px;
    &-os {
      &.ios {
        color: $drpurple-nav;
        background: $brand-yellow;
        width: 44px;
        height: 44px;
        padding: 14px 24px;
        background-image: url("../assets/ios-white.svg") !important;
        background-size: cover;
        background-position: center;
        background-size: 16px;
        background-repeat: no-repeat;
        &:hover {
          background-color: $yellow-focus;
        }
        &:focus {
          background-color: $yellow-focus;
        }
        &:disabled {
          color: $brand-yellow;
          background: $yellow-disabled;
        }
      }
      &.android {
        width: 44px;
        height: 44px;
        padding: 14px 24px;
        background-image: url("../assets/android-white.svg") !important;
        background-size: cover;
        background-position: center;
        background-size: 16px;
        background-repeat: no-repeat;
        margin-right: 16px;
      }
    }
    & .navbar-nav {
      margin-bottom: 0 !important;
          margin-top: 29px;
      & li {
        width: 100%;
        padding: 16px 0;
        border-bottom: 1px solid $line-nav;
        display: flex;
        justify-content: center;
        &:hover {
          background-color: $purple-focus;
        }
        &.nav-item a {
          color: $white;
          margin: 0;

          &::after {
            display: none;
          }
        }
      }
    }
  }
}

@media screen and (min-width: 768px) and (max-width: 990px) {
  .logo {
    width: 120.6px;
    margin-right: 34.34px;
  }
  .user {
    position: absolute;
    z-index: 2;
    width: 100%;
    padding-top: 40px;
    &-btn {
      margin-right: -19px;
    }
    &-os {
      &.ios {
        color: $drpurple-nav;
        background: $brand-yellow;
        text-align: center;
        font-size: 16px;
        font-weight: 600;
        line-height: 24px;
        width: 44px;
        height: 44px;
        padding: 14px 24px;
        background-image: url("../assets/ios-white.svg") !important;
        background-size: cover;
        background-position: center;
        background-size: 16px;
        background-repeat: no-repeat;
        &:hover {
          background-color: $yellow-focus;
        }
        &:focus {
          background-color: $yellow-focus;
        }
        &:disabled {
          color: $brand-yellow;
          background: $yellow-disabled;
        }
      }
      &.android {
        width: 44px;
        height: 44px;
        padding: 14px 24px;
        background-image: url("../assets/android-white.svg") !important;
        background-size: cover;
        background-position: center;
        background-size: 16px;
        background-repeat: no-repeat;
        margin-right: 16px;
      }
    }
    & .navbar-nav {
      margin-bottom: 0 !important;
      & li {
        width: 100%;
        padding: 16px 0;
        border-bottom: 1px solid $line-nav;
        display: flex;
        justify-content: center;
        & a {
          &::after {
            display: none;
          }
        }
        & .nav-item a {
          color: $white;
        }
      }
    }
  }
  .owner {
    position: absolute;
    z-index: 2;
    padding-top: 40px;
    width: 100%;
    &-bar {
      width: 100%;
    }
    & .navbar-nav {
      margin-bottom: 0 !important;
      & li {
        width: 100%;
        padding: 16px 0;
        border-bottom: 1px solid $line-nav;
        display: flex;
        justify-content: center;
        &.nav-item a {
          color: $white;
          margin: 0;
        }
      }
    }
    &-os {
      &.ios {
        color: $drpurple-nav;
        background: $brand-yellow;
        text-align: center;
        font-size: 16px;
        font-weight: 600;
        line-height: 24px;
        width: 44px;
        height: 44px;
        padding: 14px 24px;
        background-image: url("../assets/ios-white.svg") !important;
        background-size: cover;
        background-position: center;
        background-size: 16px;
        background-repeat: no-repeat;
        &:hover {
          background-color: $yellow-focus;
        }
        &:focus {
          background-color: $yellow-focus;
        }
        &:disabled {
          color: $brand-yellow;
          background: $yellow-disabled;
        }
      }
      &.android {
        width: 44px;
        height: 44px;
        padding: 14px 24px;
        background-image: url("../assets/android-white.svg") !important;
        background-size: cover;
        background-position: center;
        background-size: 16px;
        background-repeat: no-repeat;
        margin-right: 16px;
      }
    }
  }
}
@media screen and (min-width: 1200px) {
  .user {
    background: transparent !important;
    & .user-os.android {
      margin-left:66px;
    }
  }
  .owner {
    background: transparent !important;
   }
   .communication-title {
    margin-top: 119px!important;
  }
}
</style>
