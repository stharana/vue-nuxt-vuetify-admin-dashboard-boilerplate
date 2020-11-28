<template>
  <v-form v-model="valid">
    <v-layout row wrap>
      <v-flex sm12 lg12 md12>
        <v-subheader class="pa-0 mt-3">CONTACT DETAIL</v-subheader>
      </v-flex>
      <v-flex sm12 lg3 md3>
        <v-text-field
          label="Company Name"
          placeholder="Enter company name here"
          name="companyname"
          v-model="formModel.companyname"
          v-validate="'required'"
          data-vv-name="companyname"
          :error-messages="errors.collect('companyname')"
          required
        ></v-text-field>
      </v-flex>
      <v-flex sm12 lg3 md3>
        <v-text-field
          label="Contact Person Name"
          placeholder="Enter contact person name here"
          name="fullname"
          v-model="formModel.name"
          v-validate="'required'"
          data-vv-name="fullname"
          :error-messages="errors.collect('fullname')"
          required
        ></v-text-field>
      </v-flex>
      <v-flex sm12 lg3 md3>
        <v-text-field
          label="Email"
          name="email"
          placeholder="example@gmail.com"
          v-validate="'required|email'"
          data-vv-name="email"
          :error-messages="errors.collect('email')"
          v-model="formModel.email"
          required
        ></v-text-field>
      </v-flex>
      <v-flex sm12 lg3 md3> </v-flex>
      <v-flex sm12 lg3 md3>
        <v-text-field
          label="Mobile Phone"
          placeholder="(###) ### - ####"
          v-validate="'required'"
          data-vv-name="mobilephone"
          :error-messages="errors.collect('mobilephone')"
          v-model="formModel.mobilephone"
          mask="phone"
          required
        ></v-text-field>
      </v-flex>
      <v-flex sm12 lg3 md3>
        <v-text-field
          label="Telephone"
          placeholder="(###) ### - ####"
          v-validate="'required'"
          data-vv-name="telephone"
          :error-messages="errors.collect('telephone')"
          v-model="formModel.telephone"
          mask="phone"
          required
        ></v-text-field>
      </v-flex>
      <v-flex sm12 lg12 md12>
        <v-subheader class="pa-0 mt-3">ADDRESS</v-subheader>
      </v-flex>
      <v-flex sm12 lg3 md3>
        <v-select
          placeholder="Select a country"
          :items="countries"
          v-validate="'required'"
          data-vv-name="country"
          :error-messages="errors.collect('country')"
          v-model="formModel.country"
          label="Country"
          required
          item-text="country"
          item-value="abbr"
        ></v-select>
      </v-flex>
      <v-flex sm12 lg3 md3>
        <v-text-field
          placeholder="Enter state here"
          v-validate="'required'"
          data-vv-name="state"
          :error-messages="errors.collect('state')"
          v-model="formModel.state"
          label="State"
          required
        ></v-text-field>
      </v-flex>
      <v-flex sm12 lg3 md3>
        <v-text-field
          placeholder="Enter city here"
          v-validate="'required'"
          data-vv-name="city"
          :error-messages="errors.collect('city')"
          v-model="formModel.city"
          label="City"
          required
        ></v-text-field>
      </v-flex>
      <v-flex sm12 lg3 md3>
        <v-text-field
          placeholder="Enter zipcode here"
          label="Zip Code"
          v-model="formModel.zipcode"
          required
        ></v-text-field>
      </v-flex>
      <v-flex sm12 lg6 md6>
        <v-text-field
          placeholder="Enter address here"
          label="Address"
          v-validate="'required'"
          data-vv-name="address"
          :error-messages="errors.collect('address')"
          v-model="formModel.address"
          required
        ></v-text-field>
      </v-flex>
      <v-flex sm12 lg6 md6></v-flex>
      <v-flex sm12 lg12 md12>
        <v-subheader class="pa-0 mt-3">STANDARDS</v-subheader>
      </v-flex>
      <v-flex sm12 lg3 md3>
        <v-select
          :items="standards"
          v-model="formModel.standards"
          chips
          multiple=""
          label="Applying For"
          placeholder="Select standards"
          class="input-group--focused"
          item-text="name"
          item-value="id"
          v-validate="'required'"
          data-vv-name="standards"
          required
          :error-messages="errors.collect('standards')"
        ></v-select>
      </v-flex>
      <v-flex sm12 lg6 md6>
        <v-textarea
          placeholder="Enter brief explanation of process"
          v-validate="'required'"
          data-vv-name="description"
          :error-messages="errors.collect('description')"
          v-model="formModel.description"
          label="Description"
          required
        ></v-textarea>
      </v-flex>
    </v-layout>
    <div class="form-btn">
      <v-btn @click="submit" color="success">Submit</v-btn>
      <v-btn @click="clear">Clear</v-btn>
    </div>
  </v-form>
</template>

<script>
import Countries from "@/api/country";
export default {
  data: () => ({
    $_veeValidate: {
      validator: "new"
    },
    formModel: {
      country: null
    },
    countries: Countries,
    standards: [
      { name: "GRS", id: 1 },
      { name: "RCS", id: 2 },
      { name: "OCS", id: 3 },
      { name: "RDS", id: 4 },
      { name: "RWS", id: 5 },
      { name: "CCS", id: 6 }
    ],
    valid: true
  }),
  mounted() {
    this.$validator.localize("en", this.dictionary);
  },
  methods: {
    submit() {
      this.$validator.validateAll();
      console.log(this.formModel);
    },
    clear() {
      this.formModel = {};
      this.$validator.reset();
    }
  }
};
</script>
