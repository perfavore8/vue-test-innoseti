<template>
  <div id="app">
    <nav :class="{ navShort: !fullNav, navFull: fullNav }">
      <button @click="toggleNav()" class="btn">
        <img
          src="./assets/cross.png"
          :alt="firstLetter"
          class="icon"
          v-if="fullNav"
        />
        <img src="./assets/navbar.png" :alt="firstLetter" class="icon" v-else />
      </button>
      <router-link
        v-for="nav in navList"
        :key="nav.name"
        :to="nav.link"
        v-show="fullNav"
      >
        {{ nav.name }}
      </router-link>
    </nav>
    <router-view>
      <h1>Колличество переходов - {{ count }}</h1>
    </router-view>
  </div>
</template>

<script>
import Data from "./Data.json";
export default {
  data() {
    return {
      fullNav: true,
      navList: Data,
    };
  },

  computed: {
    count() {
      return this.$store.state.counter;
    },
    firstLetter() {
      if (this.navList.length) {
        return this.navList[0].name.split("")[0];
      }
      return "";
    },
  },

  mounted() {
    this.fullNav = JSON.parse(localStorage.getItem("fullNav"));
    // this.getNavListData();
  },

  watch: {
    $route(from, to) {
      if (to.name != null) this.$store.commit("increase");
    },
  },

  methods: {
    toggleNav() {
      this.fullNav = !this.fullNav;
      localStorage.setItem("fullNav", JSON.stringify(this.fullNav));
    },
    // getNavListData() {
    //   fetch("./DATA.json")
    //     .then((response) => response.json())
    //     .then((data) => (this.navList = data));
    // },
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
}

.navShort {
  min-height: none;
  height: min-content;
  overflow: hidden;
}

.navFull {
  min-height: calc(100vh - 1em);
  height: 100%;
}

nav {
  display: flex;
  flex-direction: column;
  border: 1px solid #2c3e50;
  border-radius: 0.5em;
  margin: 0.5em;
  min-width: 8%;
  max-width: 20%;
  background-color: #ecf4f5f9;
  gap: 1.25em;
  padding: 1em;
  margin-right: 2em;
  // position: absolute;
  // top: 0;
  // left: 0;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
.btn {
  width: 2.5em;
  height: 2.5em;
  padding: 0.25em;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto;
  outline: none;
  border: none;
  background-color: transparent;
  .icon {
    width: 100%;
    height: 100%;
  }
}
</style>
