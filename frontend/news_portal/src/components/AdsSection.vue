<template>
  <v-card
    elevation="4"
    class="my-5"
  >
    <v-img
      src="../assets/adsSection/original.jpg"
      lazy-src="../assets/adsSection/lazy.jpg"
      max-width="100vw"
      height="200"
      max-height="250"
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
      <v-row
        class="fill-height ma-0"
        align="center"
        justify="end"
      >
        <v-col
          cols="4"
        >
          <div
            class="d-flex display-2 white--text font-weight-black"
          >
            Shop The Best. <br>
            Get The Best.
          </div>
        </v-col>
      </v-row>
    </v-img>
  </v-card>
</template>

<script>
export default {

}
</script>
