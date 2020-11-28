<template>
  <v-card ref="form">
    <v-toolbar color="success" dark flat dense cad>
      <v-toolbar-title class="subheading">Ship Form</v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>
    <v-card-text>
      <v-flex sm4 lg4>
        <v-text-field
          label="Full Name"
          placeholder="John Doe"
          v-model="name"
          required
          ref="name"
          :rules="[() => !!name || 'This field is required']"
          :error-messages="errorMessages"
        ></v-text-field>
      </v-flex>
      <v-flex sm4 lg4>
        <v-text-field
          label="Address Line"
          placeholder="Snowy Rock Pl"
          :rules="[
            () => !!address || 'This field is required',
            () =>
              (!!address && address.length <= 25) ||
              'Address must be less than 25 characters',
            addressCheck
          ]"
          v-model="address"
          ref="address"
          counter="25"
          required
        ></v-text-field>
      </v-flex>
      <v-text-field
        label="City"
        placeholder="El Paso"
        :rules="[() => !!city || 'This field is required', addressCheck]"
        v-model="city"
        ref="city"
        required
      ></v-text-field>
      <v-text-field
        label="State/Province/Region"
        v-model="state"
        :rules="[() => !!state || 'This field is required']"
        required
        ref="state"
        placeholder="TX"
      ></v-text-field>
      <v-text-field
        label="ZIP / Postal Code"
        required
        :rules="[() => !!zip || 'This field is required']"
        v-model="zip"
        ref="zip"
        placeholder="79938"
      ></v-text-field>
      <v-select
        autocomplete
        label="Country"
        placeholder="Select..."
        :rules="[() => !!country || 'This field is required']"
        :items="countries"
        v-model="country"
        ref="country"
        required
      ></v-select>
    </v-card-text>
    <v-divider class="mt-5"></v-divider>
    <v-card-actions>
      <!-- <v-spacer></v-spacer> -->
      <v-slide-x-reverse-transition>
        <v-tooltip left v-if="formHasErrors">
          <v-btn icon @click="resetForm" slot="activator" class="my-0">
            <v-icon>refresh</v-icon>
          </v-btn>
          <span>Refresh form</span>
        </v-tooltip>
      </v-slide-x-reverse-transition>
      <v-btn color="info" flat @click="submit">Submit</v-btn>
      <v-btn flat>Cancel</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  data: () => ({
    countries: [
      "Afghanistan",
      "Vietnam",
      "Virgin Islands (US)",
      "Yemen",
      "Zambia",
      "Zimbabwe"
    ],
    errorMessages: [],
    name: null,
    address: null,
    city: null,
    state: null,
    zip: null,
    country: null,
    formHasErrors: false
  }),

  computed: {
    form() {
      return {
        name: this.name,
        address: this.address,
        city: this.city,
        state: this.state,
        zip: this.zip,
        country: this.country
      };
    }
  },

  watch: {
    name() {
      this.errorMessages = [];
    }
  },

  methods: {
    addressCheck() {
      this.errorMessages =
        this.address && !this.name ? ["Hey! I'm required"] : [];

      return true;
    },
    resetForm() {
      this.errorMessages = [];
      this.formHasErrors = false;

      Object.keys(this.form).forEach(f => {
        this.$refs[f].reset();
      });
    },
    submit() {
      this.formHasErrors = false;
      Object.keys(this.form).forEach(f => {
        if (!this.form[f]) this.formHasErrors = true;

        this.$refs[f].validate(true);
      });
    }
  }
};
</script>
