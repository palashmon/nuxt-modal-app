<template>
  <v-container>
    <v-form ref="form" @submit.prevent="validate" id="validate-form">
      <v-row>
        <v-col cols="12" sm="6" md="6">
          <v-text-field
            label="First name*"
            v-model.trim="firstName"
            required
            :error-messages="getErrors('firstName', $v.firstName)"
            @blur="$v.firstName.$touch()"
          ></v-text-field>
        </v-col>
        <v-col cols="12" sm="6" md="6">
          <v-text-field
            label="Last name*"
            v-model.trim="lastName"
            required
            :error-messages="getErrors('lastName', $v.lastName)"
            @blur="$v.lastName.$touch()"
          ></v-text-field>
        </v-col>
        <v-col cols="12">
          <v-text-field
            label="Email*"
            required
            v-model.trim="email"
            :error-messages="getErrors('email', $v.email)"
            @blur="$v.email.$touch()"
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
import { required, minLength, email } from "vuelidate/lib/validators";
export default {
  mixins: [validationMixin],
  data: () => ({
    firstName: "",
    lastName: "",
    email: ""
  }),

  validations: {
    firstName: { required },
    lastName: { required },
    email: { required, email }
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
        case "firstName":
          !model.required && errors.push("First name is required.");
          break;
        case "lastName":
          !model.required && errors.push("Last name is required.");
          break;
        case "email":
          !model.email && errors.push("Must be valid e-mail");
          !model.required && errors.push("E-mail is required");
          break;
        default:
          break;
      }
      return errors;
    }
  }
};
</script>
