<template>
  <v-container>
    <div id="map"></div>
    <div class="mt-2">
      <v-text-field
        label="Search For Address"
        box
        color="success"
        class="ml-1 mr-1"
        style="max-width: 200px;"
      ></v-text-field>
      <div style="display: flex; flex-direction: row;">
        <v-select
          :items="zipItems"
          box
          label="Zipcode"
          color="success"
          style="max-width: 160px;"
          class="ml-1 mr-1"
        ></v-select>
        <v-text-field
          label="Min Current Land"
          box
          color="success"
          class="ml-1 mr-1"
          style="max-width: 200px;"
        ></v-text-field>
        <v-text-field
          label="Max Current Land"
          box
          color="success"
          class="ml-1 mr-1"
          style="max-width: 200px;"
        ></v-text-field>
      </div>
      <v-btn color="info" @click="removeLocation()">Apply Filters</v-btn>
    </div>
  </v-container>
</template>

<script >
// const markersData = require("../AddressInfo");
const markersData = require("../dataCleanedUpdated.js");

export default {
  data() {
    return {
      previousMarker: null,
      markers: markersData.markers,
      allMarkers: [],
      zipItems: ["Any Zipcode", "60613", "60614", "60615"]
    };
  },
  mounted() {
    // console.log(this.markers[0]);
    this.initMap();
  },
  methods: {
    current_land_filter(value) {
      console.log(value);
    },
    showAll() {
      this.allMarkers.forEach(address => {
        address.setVisible(true);
      });
    },
    removeTwoBathrooms() {
      this.markers.forEach((address, i) => {
        if (address.properties.bathrooms == 2) {
          this.allMarkers[i].setVisible(false);
          if (this.previousMarker == this.allMarkers[i]) {
            this.previousMarker.infowindow.close();
          }
        }
      });
    },
    initMap() {
      // Map options
      var options = {
        zoom: 12,
        center: { lat: 41.9, lng: -87.6676657 }
      };
      // New Map
      var map = new google.maps.Map(document.getElementById("map"), options);

      // Loops through markers
      this.markers.forEach(address => {
        var marker = new google.maps.Marker({
          position: address.coords,
          map: map,
          visible: address.visible
        });

        // Add markers with colors

        if (address.properties.ESTIMATED_MARKET_VALUE <= 400000) {
          marker.setIcon(
            "https://maps.google.com/mapfiles/ms/icons/red-dot.png"
          );
        }

        if (
          address.properties.ESTIMATED_MARKET_VALUE > 400000 &&
          address.properties.ESTIMATED_MARKET_VALUE <= 450000
        ) {
          marker.setIcon(
            "https://maps.google.com/mapfiles/ms/icons/orange-dot.png"
          );
        }

        if (
          address.properties.ESTIMATED_MARKET_VALUE > 450000 &&
          address.properties.ESTIMATED_MARKET_VALUE <= 525000
        ) {
          marker.setIcon(
            "https://maps.google.com/mapfiles/ms/icons/yellow-dot.png"
          );
        }

        if (address.properties.ESTIMATED_MARKET_VALUE > 525001) {
          marker.setIcon(
            "https://maps.google.com/mapfiles/ms/icons/green-dot.png"
          );
        }

        if (address.content) {
          marker.infowindow = new google.maps.InfoWindow({
            content: address.content
          });
          marker.addListener("click", () => {
            marker.infowindow.open(map, marker);
            if (this.previousMarker) {
              this.previousMarker.infowindow.close();
              if (this.previousMarker == marker) {
                marker.infowindow.open(map, marker);
              }
            }

            this.previousMarker = marker;
          });
        }
        this.allMarkers.push(marker);
      });
    }
  }
};
</script>

<style>
#map {
  height: 400px;
  width: 100%;
}
</style>
