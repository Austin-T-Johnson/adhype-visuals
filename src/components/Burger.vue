<template>
  <div class="container show-mobile">
    <div class="burger-container">
      <button
        v-bind:class="[isActive ? 'hamburger--3dx is-active' : 'hamburger']"
        @click="toggleActive()"
        type="button"
      >
        <span class="hamburger-box">
          <span
            class="hamburger-inner"
            :class="{ 'inner-active': isActive }"
          ></span>
        </span>
      </button>
    </div>

    <div class="mobile-nav" v-if="isActive">
      <router-link @click="toggleActive()" class="nav" to="/"><li>Home</li></router-link>
      <router-link @click="toggleActive()" class="nav" to="/about"><li>About</li></router-link>
      <router-link @click="toggleActive()" class="nav" to="/design"><li>Design</li></router-link>
      <router-link @click="toggleActive()" class="nav" to="/contact"><li>Contact</li></router-link>
    </div>
  </div>
</template>
<script>
export default {
  name: "hamBurger",
  data() {
    return {
      isActive: false,
    };
  },
  mounted() {},
  methods: {
    toggleActive() {
      this.isActive = !this.isActive;
    },
  },
  computed: {},
};
</script>
<style scoped lang="scss">
@media (max-width: 728px) {
  .container {
    width: 50%;
    z-index: 4;
    position: absolute;
    top: 0;
    right: 0;
  }

  .burger-container {
    width: 100%;
    position: absolute;
    top: 0;
    padding-right: 2%;
    display: flex;
    justify-content: right;
    gap: 15px;
    align-items: center;
    z-index: 5;
  }
  .nav {
    text-decoration: none;
    color: black;
    list-style: none;
    font-size: 2rem;
    line-height: 250%;
  }
  .mobile-nav {
    height: 100vh;
    width: 100%;
    background-color: $white;
    padding-top: 25%;
  }

  .hamburger {
    padding: 15px 15px;
    display: inline-block;
    cursor: pointer;
    transition-property: opacity, filter;
    transition-duration: 0.15s;
    transition-timing-function: linear;
    font: inherit;
    text-transform: none;
    background-color: transparent !important;
    border: 0;
    margin: 0;
  }
  .hamburger:hover {
    opacity: 0.7;
  }
  .hamburger.is-active:hover {
    opacity: 0.7;
  }

  .hamburger-box {
    width: 40px;
    height: 24px;
    display: inline-block;
    position: relative;
  }

  .hamburger-inner {
    display: block;
    top: 50%;
    margin-top: -2px;
    &.inner-active {
      &::before {
        background-color: black !important;
      }
      &::after {
        background-color: black !important;
      }
    }
  }
  .hamburger-inner,
  .hamburger-inner::before,
  .hamburger-inner::after {
    width: 40px;
    height: 4px;
    background-color: $white;

    border-radius: 4px;
    position: absolute;
    transition-property: transform;
    transition-duration: 0.15s;
    transition-timing-function: ease;
  }
  .hamburger-inner::before,
  .hamburger-inner::after {
    content: "";
    display: block;
  }
  .hamburger-inner::before {
    top: -10px;
  }
  .hamburger-inner::after {
    bottom: -10px;
  }

  /*
   * 3DX
   */
  .hamburger--3dx .hamburger-box {
    perspective: 80px;
  }

  .hamburger--3dx .hamburger-inner {
    transition: transform 1.15s cubic-bezier(0.645, 0.045, 0.355, 1),
      background-color 0s 0.1s cubic-bezier(0.645, 0.045, 0.355, 1);
  }
  .hamburger--3dx .hamburger-inner::before,
  .hamburger--3dx .hamburger-inner::after {
    transition: transform 0s 0.1s cubic-bezier(0.645, 0.045, 0.355, 1);
  }

  .hamburger--3dx.is-active .hamburger-inner {
    background-color: transparent !important;
    transform: rotateY(180deg);
  }
  .hamburger--3dx.is-active .hamburger-inner::before {
    transform: translate3d(0, 10px, 0) rotate(45deg);
  }
  .hamburger--3dx.is-active .hamburger-inner::after {
    transform: translate3d(0, -10px, 0) rotate(-45deg);
  }
}
</style>




