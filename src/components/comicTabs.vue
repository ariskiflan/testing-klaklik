<template>
  <div>
    <div>
      <form @submit.prevent="search">
        <div class="form-box">
          <input
            type="search"
            v-model="parameter.keyword"
            placeholder="Search..."
            class="input-search"
          />
          <button type="submit" class="btn-search">Search</button>
        </div>
      </form>
    </div>

    <div class="grid">
      <div v-for="data in datas" :key="data">
        <img :src="data.thumbnail" alt="gambar" class="img" />
        <p class="title">{{ data.title }}</p>
      </div>
    </div>

    <div>
      <button
        v-if="info.total > parameter.limit"
        class="btn"
        @click="increaseLimit"
      >
        Show More
      </button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ComicTabsVue",
  data() {
    return {
      parameter: {
        limit: 10,
        offset: 0,
        keyword: "",
        all: "",
      },
      datas: [],
      info: {},
    };
  },
  methods: {
    async search() {
      this.parameter.limit = 10;
      await this.fetchData();
    },
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
        this.info = res.data.DATA.find((item) => item.title === "Comic");
        this.datas = this.info.data;
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

.input-search {
  width: 100%;
  height: 50px;
  border-radius: 10px;
  border: solid 1px #000;
  padding-left: 10px;
  font-size: 16px;
}

.form-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.btn-search {
  width: 10%;
  height: 50px;
  border-radius: 10px;
  border: solid 1px #000;
  color: #fff;
  font-size: 16px;
  margin-top: 20px;
  margin-bottom: 20px;
}

.btn {
  width: 10%;
  height: 50px;
  border-radius: 10px;
  border: solid 1px #000;
  color: #000;
  font-size: 16px;
  margin-top: 20px;
}
</style>
