<template>
  <v-container>
    <v-form ref="form" @submit.prevent="validate" id="validate-form">
      <v-row>
        <v-col cols="12" sm="6" md="6">
          <v-text-field
            label="Full name*"
            v-model.trim="fullName"
            required
            :error-messages="getErrors('fullName', $v.fullName)"
            @blur="$v.fullName.$touch()"
          ></v-text-field>
        </v-col>
        <v-col cols="12" sm="6" md="6">
          <v-text-field
            label="Username*"
            v-model.trim="username"
            required
            :error-messages="getErrors('username', $v.username)"
            @blur="$v.username.$touch()"
          ></v-text-field>
        </v-col>
        <v-col cols="12" sm="6" md="6">
          <v-text-field
            label="Password*"
            required
            type="password"
            v-model.trim="password"
            :error-messages="getErrors('password', $v.password)"
            @blur="$v.password.$touch()"
          ></v-text-field>
        </v-col>
        <v-col cols="12" sm="6" md="6">
          <v-text-field
            label="Confirm Password*"
            type="password"
            v-model.trim="confirmPassword"
            :error-messages="getErrors('confirmPassword', $v.confirmPassword)"
            @blur="$v.confirmPassword.$touch()"
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
import { required, minLength, sameAs } from "vuelidate/lib/validators";
export default {
  mixins: [validationMixin],
  data: () => ({
    fullName: "",
    username: "",
    password: "",
    confirmPassword: ""
  }),

  validations: {
    fullName: { required },
    username: { required },
    password: { required, minLength: minLength(4) },
    confirmPassword: { sameAsPassword: sameAs("password") }
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
        case "fullName":
          !model.required && errors.push("Full name is required.");
          break;
        case "username":
          !model.required && errors.push("Username is required.");
          break;
        case "password":
          !model.minLength &&
            errors.push("Password must be at least 4 characters long");
          !model.required && errors.push("Password is required");
          break;
        case "confirmPassword":
          !model.sameAsPassword && errors.push("Passwords must be identical");
          break;
        default:
          break;
      }
      return errors;
    }
  }
};
</script>
