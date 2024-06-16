<template>
  <div id="app">
    <h1 class="heading">Testing klaklik</h1>

    <div class="tabs-box">
      <Tabs />
    </div>
  </div>
</template>

<script>
import Tabs from "./components/tabs.vue";

export default {
  name: "App",
  components: {
    Tabs,
  },
  data() {
    return {};
  },
  methods: {},
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.heading {
  margin-bottom: 50px;
}

.tabs-box {
  margin-top: 30px;
}
</style>
