<template>
  <v-card>
    <v-tabs v-model="tab" bg-color="#fff" align-tabs="center">
      <v-tab value="one">All</v-tab>
      <v-tab value="two">Novel</v-tab>
      <v-tab value="three">Comic</v-tab>
      <v-tab value="four">Member</v-tab>
      <v-tab value="five">Forum</v-tab>
    </v-tabs>

    <v-card-text>
      <v-tabs-window v-model="tab">
        <v-tabs-window-item value="one"> <Alltabs /> </v-tabs-window-item>
        <v-tabs-window-item value="two"> <NovelTabs /> </v-tabs-window-item>
        <v-tabs-window-item value="three"> <ComicTabs /> </v-tabs-window-item>
        <v-tabs-window-item value="four"> <MemberTabs /> </v-tabs-window-item>
        <v-tabs-window-item value="five"> <ForumTabs /> </v-tabs-window-item>
      </v-tabs-window>
    </v-card-text>
  </v-card>
</template>

<script>
import NovelTabs from "./novelTabs.vue";
import ComicTabs from "./comicTabs.vue";
import Alltabs from "./alltabs.vue";
import MemberTabs from "./memberTabs.vue";
import ForumTabs from "./forumTabs.vue";

export default {
  name: "tabsVue",
  components: {
    NovelTabs,
    ComicTabs,
    Alltabs,
    MemberTabs,
    ForumTabs,
  },
  data() {
    return {
      tab: null,
    };
  },
};
</script>
