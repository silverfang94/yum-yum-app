<template>
  <span>
    <v-navigation-drawer app v-model="drawer" class="brown lighten-2" dark disable-resize-watcher>
      <v-list>
        <template v-for="(item, index) in items">
          <v-list-tile :key="index">
            <v-list-tile-content>{{item.title}}</v-list-tile-content>
          </v-list-tile>
          <v-divider :key="`divider-${index}`"></v-divider>
        </template>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar app color="brown darken-4" dark>
      <v-toolbar-side-icon class="hidden-md-and-up" @click="drawer = !drawer"></v-toolbar-side-icon>
      <v-spacer class="hidden-md-and-up"></v-spacer>
      <v-toolbar-title data-cy="titleBtn">{{appTitle}}</v-toolbar-title>
      <v-btn flat class="hidden-sm-and-down nav-menu" to="/recipes" data-cy="menuBtn">Recipes</v-btn>
      <v-spacer class="hidden-sm-and-down"></v-spacer>
      <div v-if="!isAuthenticated" class="hidden-sm-and-down">
        <v-btn flat to="/sign-in" data-cy="signinBtn">SIGN IN</v-btn>
        <v-btn color="brown lighten-3" to="/signup" class="nav-join" data-cy="joinBtn">SIGN UP</v-btn>
      </div>
      <div v-else>
        <v-btn flat to="/ingredients">Ingredients</v-btn>
        <v-btn outline color="white" @click="logout" data-cy="logout">Logout</v-btn>
      </div>
    </v-toolbar>
  </span>
</template>

<script>
export default {
  data() {
    return {
      appTitle: "Yum Yum",
      drawer: false,
      items: [
        { title: "Recipes" },
        { title: "Ingredients" },
        { title: "Sign In" },
        { title: "Sign Up" }
      ]
    };
  },
  computed: {
    isAuthenticated() {
      return this.$store.getters.isAuthenticated;
    }
  },
  methods: {
    logout() {
      this.$store.dispatch("userSignOut");
    }
  }
};
</script>

<style scoped>
a {
  color: white;
  text-decoration: none;
}
</style>
