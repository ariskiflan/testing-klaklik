<template>
  <div class="">
    <div v-for="data in datas" :key="data" class="section-category">
      <SectionCategory :datas="data.data" :title="data.title" />
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
        this.datas = res.data.DATA;
      } catch (error) {
        console.log(error);
      }
    },
  },

  mounted() {
    console.log("helllo  world");
    console.log("datas", this.datas);
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

.section-category {
  margin-bottom: 50px;
  display: flex;
  flex-direction: column;
}
</style>
