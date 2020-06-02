<template>
  <v-app id="inspire" style="background: #F5F5F5;">
    <v-content>
      <v-toolbar dark dense short color="primary">
        <v-app-bar-nav-icon></v-app-bar-nav-icon>
        <v-toolbar-title>Modal Demo App</v-toolbar-title>
        <v-spacer></v-spacer>

        <v-btn-toggle v-model="toggle_exclusive" background-color="primary" dark dense group>
          <v-btn
            v-for="item in nav"
            :key="item.title"
            :value="item.id"
            :to="item.to"
            text
          >{{ item.title }}</v-btn>
        </v-btn-toggle>
      </v-toolbar>

      <v-container fluid>
        <transition>
          <nuxt />
        </transition>
      </v-container>

      <v-footer fixed app dark color="primary darken-1">
        <span>&copy; {{ new Date().getFullYear() }}</span>
      </v-footer>
    </v-content>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      title: "Learning Nuxt.js",
      nav: [
        {
          id: 1,
          icon: "mdi-apps",
          title: "Welcome",
          to: "/"
        },
        {
          id: 1,
          icon: "mdi-apps",
          title: "Modals",
          to: "/modals"
        }
      ],
      toggle_exclusive: 1
    };
  },
  transition: {
    name: "fade-transition",
    mode: "out-in"
  }
};
</script>


