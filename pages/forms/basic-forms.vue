<template>
  <div id="page-forms">
    <v-container grid-list-xl fluid>
      <v-layout row wrap>
        <v-flex>
           <v-card>
            <!-- <v-toolbar color="success" dark flat dense cad>
              <v-toolbar-title class="subheading">Ship Form</v-toolbar-title>
              <v-spacer></v-spacer>
            </v-toolbar> -->
            <v-divider></v-divider>
            <v-card-text class="">
              <shipment-form></shipment-form>
            </v-card-text>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
import VWidget from "@/components/VWidget";
import ContactForm from "@/components/widgets/form/ContactForm";
import ShipmentForm from "../../components/widgets/form/ShipmentForm"

export default {
  layout: "dashboard",
  components: {
    VWidget,
    ContactForm,
    ShipmentForm
  },
  data() {
    return {};
  },
  computed: {},
  methods: {}
};
</script>
