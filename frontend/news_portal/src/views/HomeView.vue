<template>
  <v-container style="width: 60%!important">
    <v-row style="margin-top: 70px!important" align="center" justify="center">
      <AdsSection />
      <HotNews />
    </v-row>
  </v-container>
</template>

<script>
import AdsSection from '../components/AdsSection.vue'
import HotNews from '../components/HotNews.vue'

export default {
  name: "HomeView",

  components: {
    AdsSection,
    HotNews,
  },
};
</script>
