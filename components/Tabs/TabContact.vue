<template>
  <v-container>
    <v-form ref="form" @submit.prevent="validate" id="validate-form">
      <v-row>
        <v-col cols="12" sm="6" md="6">
          <v-text-field
            label="Contact name*"
            v-model.trim="contactName"
            required
            :error-messages="getErrors('contactName', $v.contactName)"
            @blur="$v.contactName.$touch()"
          ></v-text-field>
        </v-col>
        <v-col cols="12" sm="6" md="6">
          <v-text-field
            label="Contact phone*"
            v-model.trim="contactPhone"
            required
            :error-messages="getErrors('contactPhone', $v.contactPhone)"
            @blur="$v.contactPhone.$touch()"
          ></v-text-field>
        </v-col>
        <v-col cols="12">
          <v-text-field
            label="Address*"
            required
            v-model.trim="address"
            :error-messages="getErrors('address', $v.address)"
            @blur="$v.address.$touch()"
          ></v-text-field>
        </v-col>
        <v-col cols="12">
          <v-btn color="primary darken-1" dark type="submit" form="validate-form">Save</v-btn>
        </v-col>
      </v-row>
    </v-form>
  </v-container>
</template>


<script>
import { validationMixin } from "vuelidate";
import { required } from "vuelidate/lib/validators";
export default {
  mixins: [validationMixin],
  data: () => ({
    contactName: "",
    contactPhone: "",
    address: ""
  }),

  validations: {
    contactName: { required },
    contactPhone: { required },
    address: { required }
  },

  created() {
    this.$nextTick(() => {
      this.$v.$reset();
    });
  },

  methods: {
    close() {
      //this.$emit("update-modal", currDialog);
    },
    validate() {
      this.$v.$touch();
      if (this.$v.$invalid) {
        return;
      }
      this.close();
    },
    getErrors(name, model) {
      const errors = [];
      if (!model.$dirty) return errors;

      switch (name) {
        case "contactName":
          !model.required && errors.push("Contact name is required.");
          break;
        case "contactPhone":
          !model.required && errors.push("Contact phone is required.");
          break;
        case "address":
          !model.required && errors.push("Address is required");
          break;
        default:
          break;
      }
      return errors;
    }
  }
};
</script>
