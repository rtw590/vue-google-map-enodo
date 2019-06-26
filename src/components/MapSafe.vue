<template>
  <v-container>
    <v-btn color="info" @click="removeLocation()">Info</v-btn>
    <div id="map"></div>
  </v-container>
</template>

<script >
export default {
  data() {
    return {
      markers: [
        {
          coords: { lat: 41.9484, lng: -87.6553 },
          content: "<h1>Wrigley Field</h1>",
          iconImage:
            "https://developers.google.com/maps/documentation/javascript/examples/full/images/beachflag.png",
          visible: true
        },
        {
          coords: { lat: 41.8789, lng: -87.6359 },
          content: "<h1>Willis Tower</h1>",
          visible: true
        },
        {
          coords: { lat: 41.7886, lng: -87.5987 },
          visible: true
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
    },

    initMap() {
      console.log(this.markers);
      // Map options
      var options = {
        zoom: 10,
        center: { lat: 41.8781, lng: -87.6298 }
      };
      // New Map
      var map = new google.maps.Map(document.getElementById("map"), options);

      // Loops through markers
      for (var i = 0; i < this.markers.length; i++) {
        addMarker(this.markers[i]);
      }
      //Add marker function
      function addMarker(props) {
        var marker = new google.maps.Marker({
          position: props.coords,
          map: map,
          icon: props.iconImage,
          visible: props.visible
        });
        if (props.iconImage) {
          marker.setIcon(props.iconImage);
        }
        if (props.content) {
          var infoWindow = new google.maps.InfoWindow({
            content: props.content
          });
          marker.addListener("click", function() {
            infoWindow.open(map, marker);
          });
        }
      }
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
