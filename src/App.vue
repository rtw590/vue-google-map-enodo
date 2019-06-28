<template>
  <v-app>
    <v-toolbar app color="rgb(156, 204, 101)">
      <v-toolbar-title class="headline text-uppercase">
        <span>Chicago:</span>
        <!-- <span class="font-weight-light ml-2">Real Estate</span> -->
      </v-toolbar-title>
    </v-toolbar>

    <v-content>
      <Map/>
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
