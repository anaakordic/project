<template>
  <div class="navbar">
    <v-toolbar>
      <v-toolbar-title>MEALS DB</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" class="hidden-md-and-up">
        <v-icon>mdi-menu</v-icon>
      </v-app-bar-nav-icon>
      <v-toolbar-items
        class="hidden-sm-and-down"
        v-for="link in links"
        :key="link.name"
      >
        <v-btn :to="link.path" text>{{ link.name }}</v-btn>
      </v-toolbar-items>
    </v-toolbar>

    <v-navigation-drawer
      v-model="drawer"
      temporary
      absolute
      width="200"
      id="drawer"
    >
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="text-h6"> Meals</v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense nav>
        <v-list-item v-for="item in links" :key="item.name" :to="item.path" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.name }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      links: [
        { name: "Search meals ", path: "/", icon:"mdi-home" },
        { name: "Submit your meal", path: "/contact", icon:"mdi-comment-quote-outline"}
      ],
      drawer: false,
    };
  },
};
</script>

<style scoped>
.nav-btn {
  box-shadow: none;
}
</style>

