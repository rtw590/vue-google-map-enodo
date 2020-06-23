<template>
  <v-app>
    <v-toolbar app color="rgb(55, 71, 79)">
      <v-toolbar-title class="headline text-uppercase">
        <span style="color: white">Chicago:</span>
        <span style="color: white" class="font-weight-light ml-2">Real Estate</span>
        <!-- <img
          src="https://www.enodoinc.com/assets/images/logo/logo_green.svg"
          style="height: 30px;"
          alt="Enodo"
        />-->
      </v-toolbar-title>
    </v-toolbar>

    <v-content>
      <Map />
    </v-content>
  </v-app>
</template>

<script>
import Map from "./components/Map";

export default {
  name: "App",
  components: {
    Map
  },
  data() {
    return {
      //
    };
  }
};
</script>
