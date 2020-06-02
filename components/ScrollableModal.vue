<template>
  <v-dialog v-model="dialog" scrollable max-width="500px">
    <v-card>
      <v-card-title>Select Country</v-card-title>
      <v-divider></v-divider>
      <v-card-text style="height: 300px;">
        <v-radio-group v-model="dialogm1" column>
          <v-radio label="Bahamas, The" value="bahamas"></v-radio>
          <v-radio label="Bahrain" value="bahrain"></v-radio>
          <v-radio label="Bangladesh" value="bangladesh"></v-radio>
          <v-radio label="Barbados" value="barbados"></v-radio>
          <v-radio label="Belarus" value="belarus"></v-radio>
          <v-radio label="Belgium" value="belgium"></v-radio>
          <v-radio label="Belize" value="belize"></v-radio>
          <v-radio label="Benin" value="benin"></v-radio>
          <v-radio label="Bhutan" value="bhutan"></v-radio>
          <v-radio label="Bolivia" value="bolivia"></v-radio>
          <v-radio label="Bosnia and Herzegovina" value="bosnia"></v-radio>
          <v-radio label="Botswana" value="botswana"></v-radio>
          <v-radio label="Brazil" value="brazil"></v-radio>
          <v-radio label="Brunei" value="brunei"></v-radio>
          <v-radio label="Bulgaria" value="bulgaria"></v-radio>
          <v-radio label="Burkina Faso" value="burkina"></v-radio>
          <v-radio label="Burma" value="burma"></v-radio>
          <v-radio label="Burundi" value="burundi"></v-radio>
        </v-radio-group>
      </v-card-text>
      <v-divider></v-divider>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="primary darken-1" dark @click="close">Save</v-btn>
        <v-btn @click="close">Close</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
<script>
export default {
  props: {
    dialog: {
      type: Boolean,
      required: true,
      default: false
    }
  },
  data() {
    return {
      dialogm1: ""
    };
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
