<template>
  <v-container>
    <v-btn color="info" @click="removeLocation()">Remove</v-btn>
    <v-btn color="success" @click="showAll()">Show All</v-btn>
    <v-btn color="danger" @click="removeTwoBathrooms()">Remove 2 Bathrooms</v-btn>
    <div id="map"></div>
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
      allMarkers: []
    };
  },
  mounted() {
    // console.log(this.markers[0]);
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
