<template>
  <div class="grid">
    <div v-for="data in datas" :key="data">
      <img :src="data.thumbnail" alt="gambar" class="img" />
      <p class="title">{{ data.title }}</p>
    </div>

    <div>
      <button class="btn" @click="increaseLimit">Show More</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "NovelTabsVue",
  data() {
    return {
      parameter: {
        limit: 10,
        offset: 0,
        keyword: "",
        all: "",
      },
      datas: [],
    };
  },
  methods: {
    increaseLimit() {
      this.parameter.limit += 10;
      this.fetchData();
    },
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
        this.datas = res.data.DATA[0].data;
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
.grid {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  margin-top: 20px;
  row-gap: 50px;
}

.img {
  width: 200px;
  height: 300px;
}

.title {
  font-size: 20px;
  font-weight: 600;
}
</style>
