<template>
  <!-- Hello World -->
  <v-layout column align-center>
    <v-flex xs12 sm8 md6>
      <v-card class="mt-4">
        <v-card-title class="headline">Vuetify Modals</v-card-title>
        <v-card-text>
          <v-row class="mb-6" no-gutters>
            <v-col cols="12">
              The
              <code>v-dialog</code> component inform users about a specific task and may contain critical information, require decisions, or involve multiple tasks.
            </v-col>
          </v-row>

          <v-row class="mb-4" no-gutters>
            <v-col cols="12">
              <h2>Examples</h2>
              <p class="mt-2">Below is a collection of simple to complex examples.</p>
            </v-col>
          </v-row>

          <v-row class="mb-6" no-gutters>
            <v-col cols="12">
              <v-divider></v-divider>
              <v-row class="mb-6 mt-4" no-gutters>
                <v-col cols="12">
                  <h3>Simple Modal</h3>
                </v-col>
                <v-col cols="12">
                  <v-row justify="center">
                    <v-col cols="6" md="2">
                      <v-btn color="primary" dark @click.stop="dialog = true">Open Modal</v-btn>
                      <SimpleModal :dialog="dialog" @update-modal="update" />
                    </v-col>
                  </v-row>
                </v-col>
              </v-row>
              <v-divider></v-divider>

              <v-row class="mb-6" no-gutters>
                <v-col cols="12">cccc</v-col>
              </v-row>
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import SimpleModal from "@/components/SimpleModal";
export default {
  components: {
    SimpleModal
  },
  data() {
    return {
      dialog: false
    };
  },
  methods: {
    update(state) {
      this.dialog = state;
    }
  }
};
</script>
