<template>
  <v-app>
    <div v-if="loading == false">
      <AppBar/>
      <transition
        name="fade"
        mode="out-in"
      >
        <router-view />
      </transition>
    </div>
    <v-container
      fill-height
      fluid
      v-else
      width="100vw"
    >
      <v-row
        align="center"
        height="100%"
        justify="center"
      >
        <spring-spinner
          :animation-duration="3000"
          :size="60"
          color="blue"
        />
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
import { SpringSpinner } from 'epic-spinners'
import AppBar from './components/AppBar'

export default {
  name: 'App',

  components: {
    SpringSpinner,
    AppBar
  },

  data: () => ({
    loading: true
  }),
  beforeCreate () {
    setTimeout(() => { this.loading = false }, 2 * 1000)
    this.$router.beforeEach((to, from, next) => {
      this.loading = true
      next()
    })
    this.$router.afterEach(() => {
      setTimeout(() => { this.loading = false }, 0.5 * 1000)
    })
  },
  mounted () {
    const currentCursor = this
    currentCursor.loading = true
    this.$store
      .dispatch('fetchProducts')
      .then(() => (currentCursor.loading = false))
      .catch((error) => {
        console.log(error)
        currentCursor.isError = true
      })
    this.$store
      .dispatch('fetchCategories')
  }
}
</script>
<style scoped>
  .fade-enter-active,
  .fade-leave-active {
    transition-duration: 1s;
    transition-property: opacity;
    transition-timing-function: ease;
  }

  .fade-enter,
  .fade-leave-active {
    opacity: 0
  }
</style>
<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=Sora:wght@300&display=swap');
  $font-family: 'Sora', sans-serif;

  .v-application {
    [class*='text-'] {
      color: #36405a;
      font-family: $font-family, sans-serif !important;
    }
    font-family: $font-family, sans-serif !important;
  }
</style>
