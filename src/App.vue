<template>
  <div id="app">
    <h1 class="heading">Testing klaklik</h1>

    <div class="tabs-box">
      <Tabs />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Tabs from "./components/tabs.vue";

export default {
  name: "App",
  components: {
    Tabs,
  },
  data() {
    return {
      parameter: {
        limit: 10,
        offset: 0,
        keyword: "",
        all: "",
      },
      dummys: [
        {
          title: "Title 1",
          thumbnail:
            "https://i.pinimg.com/736x/59/de/48/59de48189e1ee84dc0c14b6514342cd8.jpg",
        },
        {
          title: " Title 2",
          thumbnail:
            "https://i.pinimg.com/736x/59/de/48/59de48189e1ee84dc0c14b6514342cd8.jpg",
        },
        {
          title: "  Title 3",
          thumbnail:
            "https://i.pinimg.com/736x/59/de/48/59de48189e1ee84dc0c14b6514342cd8.jpg",
        },
        {
          title: " Title 4",
          thumbnail:
            "https://i.pinimg.com/736x/59/de/48/59de48189e1ee84dc0c14b6514342cd8.jpg",
        },
        {
          title: " Title 5",
          thumbnail:
            "https://i.pinimg.com/736x/59/de/48/59de48189e1ee84dc0c14b6514342cd8.jpg",
        },
      ],
      data: [],
    };
  },
  methods: {
    async fetchData() {
      try {
        const param = new FormData();
        Object.entries(this.parameter).forEach(([key, value]) => {
          param.append(key, value);
        });
        const res = await axios.post(
          "https://dvl.klaklik.com/gateway2/newsearch?version=3",
          param,
          {
            headers: {
              "Content-Type": "multipart/form-data",
              APPTOKEN: "klaklikapptoken",
              DEV: "isme",
            },
          }
        );
        console.log(res);
        this.data = res.data.DATA;
      } catch (error) {
        console.log(error);
      }
    },
  },

  mounted() {
    this.fetchData();
  },
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

.grid {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  margin-top: 20px;
}

.img {
  width: 200px;
  height: 300px;
}

.title {
  font-size: 20px;
  font-weight: 600;
}

.btn {
  margin-top: 50px;
  width: 200px;
  height: 50px;
  background-color: #2c3e50;
  color: white;
  border-radius: 5px;
  border: none;
  font-size: 20px;
}

.tabs-box {
  margin-top: 30px;
}
</style>
