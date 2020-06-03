<template>
  <v-dialog v-model="dialog" persistent max-width="850px">
    <v-card>
      <v-toolbar flat dark color="primary">
        <v-toolbar-title>User Profile</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn icon dark @click="close">
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </v-toolbar>
      <v-card-text>
        <v-container>
          <v-form ref="form" @submit.prevent="validate" id="validate-form">
            <v-row>
              <v-col cols="12" sm="6" md="4">
                <v-text-field
                  label="First name*"
                  v-model.trim="firstName"
                  required
                  :error-messages="getErrors('firstName', $v.firstName)"
                  @blur="$v.firstName.$touch()"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="4">
                <v-text-field label="Middle name" hint="example of helper text only on focus"></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="4">
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
                <v-text-field
                  label="Password*"
                  type="password"
                  required
                  v-model="password"
                  :error-messages="getErrors('password', $v.password)"
                  @blur="$v.password.$touch()"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6">
                <v-select
                  :items="['0-17', '18-29', '30-54', '54+']"
                  label="Age*"
                  required
                  v-model="age"
                  :error-messages="getErrors('age', $v.age)"
                  @blur="$v.age.$touch()"
                ></v-select>
              </v-col>
              <v-col cols="12" sm="6">
                <v-autocomplete
                  :items="['Skiing', 'Ice hockey', 'Soccer', 'Basketball', 'Hockey', 'Reading', 'Writing', 'Coding', 'Basejump']"
                  label="Interests"
                  multiple
                ></v-autocomplete>
              </v-col>
            </v-row>
          </v-form>
        </v-container>
        <small>* indicates required field</small>
      </v-card-text>

      <v-divider></v-divider>

      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="primary darken-1" dark type="submit" form="validate-form">Save</v-btn>
        <v-btn @click="close">Close</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
<script>
import { validationMixin } from "vuelidate";
import { required, minLength, email } from "vuelidate/lib/validators";
export default {
  props: {
    dialog: {
      type: Boolean,
      required: true,
      default: false
    }
  },
  mixins: [validationMixin],
  data: () => ({
    firstName: "",
    middleName: "",
    lastName: "",
    email: "",
    password: "",
    age: null
  }),

  validations: {
    firstName: { required },
    lastName: { required },
    email: { required, email },
    password: { required, minLength: minLength(4) },
    age: { required }
  },
  watch: {
    dialog: function(val, oldVal) {
      // console.log('new: %s, old: %s', val, oldVal)
      if (val) {
        // Clear all previous validation errors
        this.$nextTick(() => {
          this.$v.$reset();
          this.$refs.form.reset();
          this.$refs.form.resetValidation();
        });
      }
    }
  },

  methods: {
    close() {
      let currDialog = this.dialog;
      currDialog = false;
      this.$emit("update-modal", currDialog);
    },
    validate() {
      this.$v.$touch();
      if (this.$v.$invalid) {
        return;
      }

      this.$nuxt.$loading.start();

      this.$nuxt.$loading.finish();
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
        case "password":
          !model.minLength &&
            errors.push("Password must be at least 4 characters long");
          !model.required && errors.push("Password is required");
          break;
        case "age":
          !model.required && errors.push("Age is required.");
          break;
        default:
          break;
      }
      return errors;
    }
  }
};
</script>
