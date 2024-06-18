<template>
  <div>
    <h1>{{ title }}</h1>
    <div class="grid">
      <div v-for="single in datas" :key="single.id" class="">
        <img
          :src="single.thumbnail"
          v-if="single.thumbnail"
          alt="gambar"
          class="img"
        />
        <img v-else :src="placeholder" alt="gambar" class="img" />
        <p class="title" v-if="single.title">{{ single.title }}</p>
        <p class="title" v-else>{{ single.member_name }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["title", "datas"],
  data() {
    return {
      placeholder:
        "https://upload.wikimedia.org/wikipedia/commons/thumb/6/65/No-Image-Placeholder.svg/1665px-No-Image-Placeholder.svg.png",
    };
  },
};
</script>

<style>
.section-container {
  display: flex;
  align-items: center;
}
</style>
