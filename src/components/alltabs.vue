<template>
  <div>
    <div>
      <form @submit.prevent="fetchData">
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

    <div class="">
      <div v-for="data in datas" :key="data" class="section-category">
        <SectionCategory :datas="data.data" :title="data.title" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SectionCategory from "./sectionCategory.vue";

export default {
  components: { SectionCategory },
  name: "alltabsVue",
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
    async fetchData() {
      try {
        const res = await axios.post(
          "https://dvl.klaklik.com/gateway2/newsearch?version=3",
          this.parameter,
          {
            headers: {
              "Content-Type": "multipart/form-data",
              APPTOKEN: "klaklikapptoken",
              DEV: "isme",
            },
          }
        );

        this.datas = res.data.DATA;
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

.section-category {
  margin-bottom: 50px;
  display: flex;
  flex-direction: column;
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
</style>
