<template>
  <v-navigation-drawer
    id="app-drawer"
    v-model="inputValue"
    app
    dark
    floating
    persistent
    mobile-break-point="991"
    width="260"
  >
    <v-img :src="image" height="100%">
      <v-layout class="fill-height" tag="v-list" column>
        <v-list-tile avatar>
          <v-list-tile-avatar color="white">
            <v-img :src="logo" height="34" contain />
          </v-list-tile-avatar>
          <v-list-tile-title class="title">林峻毅</v-list-tile-title>
        </v-list-tile>
        <v-divider />
        <v-list-tile
          v-for="(link, i) in links"
          :key="i"
          :to="link.to"
          :active-class="color"
          avatar
          class="v-list-item"
        >
          <v-list-tile-action>
            <v-icon>{{ link.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-title v-text="link.text" />
        </v-list-tile>
        <!-- <v-list-tile active-class="success" class="v-list-item v-list__tile--buy" to="/upgrade">
          <v-list-tile-action>
            <v-icon>mdi-package-up</v-icon>
          </v-list-tile-action>
          <v-list-tile-title class="font-weight-light">Upgrade To PRO</v-list-tile-title>
        </v-list-tile>-->
      </v-layout>
    </v-img>
  </v-navigation-drawer>
</template>

<script>
// Utilities
import { mapMutations, mapState } from "vuex";

export default {
  props: {
    opened: {
      type: Boolean,
      default: false
    }
  },
  data: () => ({
    logo: "favicon.ico",
    links: [
      {
        to: "/",
        icon: "mdi-view-dashboard",
        text: "Dashboard"
      },
      {
        to: "/user-profile",
        icon: "mdi-account",
        text: "Profile"
      },
      {
        to: "/skill",
        icon: "mdi-clipboard-outline",
        text: "Skill"
      },
      {
        to: "/typography",
        icon: "mdi-format-font",
        text: "Typography"
      },
      {
        to: "/notifications",
        icon: "mdi-bell",
        text: "Notifications"
      },
      {
        to: "/course",
        icon: "fas fa-shoe-prints",
        text: "Course"
      },
      {
        to: "/portfolio",
        icon: "mdi-book-open-page-variant",
        text: "Portfolio"
      }
    ]
  }),
  computed: {
    ...mapState("app", ["image", "color"]),
    inputValue: {
      get() {
        return this.$store.state.app.drawer;
      },
      set(val) {
        this.setDrawer(val);
      }
    },
    items() {
      return this.$t("Layout.View.items");
    }
  },

  methods: {
    ...mapMutations("app", ["setDrawer", "toggleDrawer"])
  }
};
</script>

<style lang="scss">
#app-drawer {
  .v-list__tile {
    border-radius: 4px;

    &--buy {
      margin-top: auto;
      margin-bottom: 17px;
    }
  }
}
</style>
