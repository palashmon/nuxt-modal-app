<template>
  <v-dialog v-model="dialog" max-width="850px">
    <v-card>
      <v-toolbar flat dark color="primary">
        <v-toolbar-title>User Details</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn icon dark @click="close">
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </v-toolbar>

      <v-card-text class="mt-4">
        <v-card>
          <v-tabs>
            <v-tab
              v-for="tab in tabs"
              :key="tab"
              :class="[{ active: currentTab === tab }]"
              @click="currentTab = tab"
            >{{ tab }}</v-tab>
          </v-tabs>
          <v-container>
            <component v-bind:is="currentTabComponent" class="tab"></component>
          </v-container>
        </v-card>
      </v-card-text>
      <v-divider></v-divider>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn @click="close">Close</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
import TabDetails from "./TabDetails";
import TabContact from "./TabContact";
import TabProfile from "./TabProfile";
export default {
  components: {
    TabDetails,
    TabContact,
    TabProfile
  },
  props: {
    dialog: {
      type: Boolean,
      required: true,
      default: false
    }
  },
  data: () => ({
    currentTab: "Details",
    tabs: ["Details", "Contact", "Profile"]
  }),
  computed: {
    currentTabComponent: function() {
      return "Tab" + this.currentTab;
    }
  },
  methods: {
    close() {
      let currDialog = this.dialog;
      currDialog = false;
      this.$emit("update-modal", currDialog);
    }
  }
};
</script>
