<template>
  <v-app-bar
    max-width="100vw"
    max-height="75"
    :color="appBarcolor"
    app
    v-scroll="changeColorOnScroll"
    elevate-on-scroll
    :dark="dark"
    height="70"
  >
    <v-toolbar-title>
      <v-btn
        text
        rounded
        to="/"
        color="transparent"
        height="70"
        v-if="mobile"
      >
        <v-img
          lazy-src="../assets/demologo.png"
          src="../assets/demologo.png"
          width="110"
          height="70"
          class="mr-2"
        >
          <template v-slot:placeholder>
            <v-row class="fill-height ma-0" align="center" justify="center">
              <v-progress-circular
                indeterminate
                color="primary"
              ></v-progress-circular>
            </v-row>
          </template>
        </v-img>
        <div :class="appBarContentColor">News Portal</div>
      </v-btn>
      <v-btn
        text
        rounded
        to="/"
        color="transparent"
        height="70"
        v-else
        class="mr-10"
      >
        <v-img
          src="../assets/demologo.png"
          width="70"
          height="30"
          class="mr-2"
        />
        <div :class="appBarContentColor">News Portal</div>
      </v-btn>
    </v-toolbar-title>
    <v-spacer />
    <div id="nav" v-if="desktop">
      <v-btn
        text
        v-for="link in routes"
        :key="link.name"
        :to="link.link"
        small
        class="font-weight-bold"
      >
        <div :class="appBarContentColor">
          {{ link.name }}
        </div>
      </v-btn>
    </div>
    <v-btn icon v-if="showSearchIcon && desktop == true" @click="showSearchIcon = false">
      <v-icon>
        mdi-magnify
      </v-icon>
    </v-btn>
    <v-btn icon v-if="mobile" @click="openSearchMobile">
      <v-icon>
        mdi-magnify
      </v-icon>
    </v-btn>
    <transition name="fade" mode="out-in" v-if="desktop == true">
      <div v-if="showSearchIcon == false">
        <v-autocomplete
          v-if="showSearchIcon == false"
          label="Search Keywords"
          placeholder="Hot keywords"
          clearable
          dense
          rounded
          solo
          class="mt-4 ml-2"
          :items="hotkeywords"
          @keydown.enter.prevent="searchButton"
        >
          <template slot="append">
            <v-icon @click="searchButton">
              mdi-magnify
            </v-icon>
          </template>
        </v-autocomplete>
      </div>
    </transition>
    <v-spacer/>
    <!-- date on the appbar -->
    <div :class="appBarContentColor" v-if="desktop">
      {{ dateVal }}
    </div>
    <v-dialog
      v-if="mobile"
      v-model="appNavDialog"
      fullscreen
      hide-overlay
      transition="dialog-bottom-transition"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-app-bar-nav-icon
          :class="appBarContentColor"
          dark
          v-bind="attrs"
          v-on="on"
        />
      </template>
      <v-card>
        <v-toolbar dark color="primary">
          <v-toolbar-title>
            <v-btn
              text
              rounded
              to="/"
              color="transparent"
              height="80"
            >
              <v-img
                src="../assets/demologo.png"
                width="70"
                height="30"
                class="mr-5"
              />
              <div class="white--text">News Portal</div>
            </v-btn>
          </v-toolbar-title>
          <v-spacer />
          <v-toolbar-items>
            <v-btn icon dark @click="appNavDialog = false">
              <v-icon>mdi-close</v-icon>
            </v-btn>
          </v-toolbar-items>
        </v-toolbar>
        <v-list dense class="primary--text font-weight-light ml-3">
          {{ dateVal }}
        </v-list>
        <v-list two-line dense>
          <v-list-item
            v-for="(links, index) in routes"
            :key="index"
            link
            :to="links.link"
            dense
          >
            <v-list-item-content>
              <v-list-item-title v-text="links.name" />
            </v-list-item-content>
          </v-list-item>
        </v-list>
        <v-list-item>
          <v-autocomplete
            label="Search Keywords"
            placeholder="Hot keywords"
            clearable
            dense
            solo
            :items="hotkeywords"
            @keydown.enter.prevent="searchButton"
          >
            <template slot="append">
              <v-icon @click="searchButton">
                mdi-magnify
              </v-icon>
            </template>
          </v-autocomplete>
        </v-list-item>
      </v-card>
    </v-dialog>
  </v-app-bar>
</template>

<script>

export default {
  name: "AppBar",
  components: {
  },
  data() {
    return {
      appNavDialog: true,
      appBarcolor: "transparent",
      dark: false,
      appBarContentColor: "blue--text font-weight-bold",
      loginDialog: false,
      registerDialog: false,
      dateVal: "Date",

      // search button variables
      isIcon: true,
      showSearchIcon: true,
      hotkeywords: ["foo", "bar", "fizz", "buzz"],
    };
  },
  methods: {
    openSearchMobile() {
      this.appNavDialog = true;
    },
    searchButton() {
      console.log("over here");
    },
    changeColorOnScroll(e) {
      if (typeof window === "undefined") return;
      const top = window.pageYOffset || e.target.scrollTop || 0;
      if (top > 20) {
        this.appBarcolor = "primary";
        this.appBarContentColor = "white--text";
        this.dark = true;
      } else {
        this.appBarcolor = "transparent";
        this.appBarContentColor = "blue--text";
        this.dark = false;
      }
    },
    dateHere() {
      var currentDate = new Date();
      const months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      const days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      this.dateVal = days[currentDate.getDay()] + " " + months[currentDate.getMonth()] + " " + currentDate.getDate() + ", " +  currentDate.getFullYear(); 
    },
  },
  mounted() {
    this.dateHere()
  },
  computed: {
    routes() {
      return [
        { name: "Vision", link: "/vision" },
        { name: "How It Works", link: "/how-it-works" },
        { name: "About", link: "/about" },
        { name: "Categories", link: "/categories" },
        { name: "Custom", link: "/custom" },
      ]
    },
    mobile() {
      if (
        this.$vuetify.breakpoint.name === "xs" ||
        this.$vuetify.breakpoint.name === "sm"
      ) {
        return true;
      }
    },
    desktop() {
      if (
        this.$vuetify.breakpoint.name === "xs" ||
        this.$vuetify.breakpoint.name === "sm"
      ) {
        return false;
      }
      else {
        return true;
      }
    },
  },
};
</script>

<style scoped>
.v-chip:hover {
  cursor: pointer;
}

  .fade-enter-active,
  .fade-leave-active {
    transition-duration: 1s;
    transition-property: opacity width;
    transition-timing-function: ease;
  }

  .fade-enter,
  .fade-leave-active {
    opacity: 0
  }

</style>
