<template>
  <v-row align="center" justify="center">
    <v-col cols="11">
      <v-card class="ma-0 pa-0 my-5" @click="link">
        <v-card-title
          class="text-center font-weight-bold"
          v-html="titleText"
        >
        </v-card-title>
          <v-img
            src="../assets/machu-picchu-file.jpg"
            lazy-src="../assets/machu-picchu-file.jpg"
            height="450"
          >
            <template v-slot:placeholder>
              <v-row
                class="fill-height ma-0"
                align="center"
                justify="center"
              >
                <v-progress-circular
                  indeterminate
                  color="grey lighten-5"
                />
              </v-row>
            </template>
          </v-img>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: "HotNews",
  data: () => ({
    text: "Machu Picchu has been called the wrong name for over 100 years. Historians reveal its true name"
  }),
  methods: {
    link() {
      console.log("ok");
    }
  },
  computed: {
    titleText() {
      const splitted = this.text.split(" ")
      var finalText = ""
      for (var i = 0; i < splitted.length; i++){
        finalText += "<nobr>" + splitted[i] + "</nobr>" + " &nbsp "
      }
      return finalText
    }
  },
}
</script>

<style>

</style>
