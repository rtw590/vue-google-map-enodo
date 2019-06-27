<template>
  <v-container>
    <v-btn color="info" @click="removeLocation()">Remove</v-btn>
    <v-btn color="success" @click="showAll()">Show All</v-btn>
    <v-btn color="danger" @click="removeTwoBathrooms()">Remove 2 Bathrooms</v-btn>
    <div id="map"></div>
  </v-container>
</template>

<script >
const markersData = require("../AddressInfo");
const markersDataFull = require("../dataCleaned.json");

console.log(markersData.markers[0]);

console.log(markersDataFull[0]);

export default {
  data() {
    return {
      previousMarker: null,
      markers: markersDataFull,
      allMarkers: []
    };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    removeLocation() {
      this.allMarkers[0].setVisible(false);
      this.allMarkers[2].setVisible(false);
      if (this.previousMarker) {
        this.previousMarker.infowindow.close();
      }
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
        zoom: 10,
        center: { lat: 41.8781, lng: -87.6298 }
      };
      // New Map
      var map = new google.maps.Map(document.getElementById("map"), options);

      // Test 1 marker
      var marker = new google.maps.Marker({
        position: this.markers[0].coords,
        map: map,
        visible: true
      });

      console.log(marker);

      this.allMarkers.push(marker);

      // Loops through markers
      // this.markers.forEach(address => {
      //   var marker = new google.maps.Marker({
      //     position: address.coords,
      //     map: map,
      //     visible: address.visible
      //   });
      //   if (address.content) {
      //     marker.infowindow = new google.maps.InfoWindow({
      //       content: address.content
      //     });
      //     marker.addListener("click", () => {
      //       marker.infowindow.open(map, marker);
      //       if (this.previousMarker) {
      //         this.previousMarker.infowindow.close();
      //         if (this.previousMarker == marker) {
      //           marker.infowindow.open(map, marker);
      //         }
      //       }

      //       this.previousMarker = marker;
      //     });
      //   }
      //   this.allMarkers.push(marker);
      // });
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
