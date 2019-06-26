<template>
  <v-container>
    <v-btn color="info" @click="removeLocation()">Remove</v-btn>
    <v-btn color="success" @click="showAll()">Show All</v-btn>
    <v-btn color="danger" @click="removeTwoBathrooms()">Remove 2 Bathrooms</v-btn>
    <div id="map"></div>
  </v-container>
</template>

<script >
export default {
  data() {
    return {
      previousMarker: null,
      markers: [
        {
          coords: { lat: 41.9484, lng: -87.6553 },
          content:
            "<h1>Wrigley Field</h1><p>1060 W Addison St, Chicago, IL 60613</p>",
          iconImage:
            "https://developers.google.com/maps/documentation/javascript/examples/full/images/beachflag.png",
          visible: true,
          properties: {
            bathrooms: 2
          }
        },
        {
          coords: { lat: 41.8789, lng: -87.6359 },
          content: "<h1>Willis Tower</h1>",
          visible: true,
          properties: {
            bathrooms: 1
          }
        },
        {
          coords: { lat: 41.7886, lng: -87.5987 },
          visible: true,
          content: "<h1>University of Chicago</h1>",
          properties: {
            bathrooms: 3
          }
        }
      ],
      allMarkers: []
    };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    removeLocation() {
      console.log(this.allMarkers);
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
        // if (this.previousMarker) {
        //   this.previousMarker.infowindow.close();
        // }
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

      // Loops through markers
      this.markers.forEach(address => {
        var marker = new google.maps.Marker({
          position: address.coords,
          map: map,
          icon: address.iconImage,
          visible: address.visible
        });
        if (address.iconImage) {
          marker.setIcon(address.iconImage);
        }
        if (address.content) {
          // var infoWindow = new google.maps.InfoWindow({
          marker.infowindow = new google.maps.InfoWindow({
            content: address.content
          });
          marker.addListener("click", () => {
            // infoWindow.open(map, marker);
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
