<template>
  <!-- Hello World -->
  <v-layout column align-center>
    <v-flex xs12 sm8 md6>
      <v-card class="mt-4">
        <v-card-title class="headline">Vuetify Modals</v-card-title>
        <v-card-text>
          <!-- Top Header Section -->
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

              <!-- Simple Modal Section -->
              <v-row class="mb-6 mt-4" no-gutters>
                <v-col cols="12">
                  <h3>Simple Modal</h3>
                </v-col>
                <v-col cols="12">
                  <v-row justify="center">
                    <v-col cols="6" md="2">
                      <v-btn color="primary" dark @click.stop="simpleModal = true">Open Modal</v-btn>
                      <SimpleModal :dialog="simpleModal" @update-modal="updateSimpleModal" />
                    </v-col>
                  </v-row>
                </v-col>
              </v-row>
              <v-divider></v-divider>

              <!-- Scrollable Modal Section -->
              <v-row class="mb-6 mt-4" no-gutters>
                <v-col cols="12">
                  <h3>Scrollable Modal</h3>
                </v-col>
                <v-col cols="12">
                  <v-row justify="center">
                    <v-col cols="6" md="2">
                      <v-btn color="primary" dark @click.stop="scrollableModal = true">Open Modal</v-btn>
                      <ScrollableModal
                        :dialog="scrollableModal"
                        @update-modal="updateScrollableModal"
                      />
                    </v-col>
                  </v-row>
                </v-col>
              </v-row>
              <v-divider></v-divider>

              <!-- Form Modal Section -->
              <v-row class="mb-6 mt-4" no-gutters>
                <v-col cols="12">
                  <h3>Form Modal</h3>
                  <p class="mt-2">Just a simple example of a form in a dialog.</p>
                </v-col>
                <v-col cols="12">
                  <v-row justify="center">
                    <v-col cols="6" md="2">
                      <v-btn color="primary" dark @click.stop="formModal = true">Open Modal</v-btn>
                      <FormModal :dialog="formModal" @update-modal="updateFormModal" />
                    </v-col>
                  </v-row>
                </v-col>
              </v-row>
              <v-divider></v-divider>

              <v-row class="mb-6 mt-4" no-gutters>
                <v-col cols="12">More...</v-col>
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
import ScrollableModal from "@/components/ScrollableModal";
import FormModal from "@/components/FormModal";
export default {
  components: {
    SimpleModal,
    ScrollableModal,
    FormModal
  },
  data() {
    return {
      simpleModal: false,
      scrollableModal: false,
      formModal: false
    };
  },
  methods: {
    updateSimpleModal(state) {
      this.simpleModal = state;
    },
    updateScrollableModal(state) {
      this.scrollableModal = state;
    },
    updateFormModal(state) {
      this.formModal = state;
    }
  }
};
</script>
