<template>
  <v-container>
    <div id="map" style="border: solid 1px rgb(201, 201, 201);" class></div>

    <v-layout row class="mt-2">
      <v-btn color="info" @click="applyFilters()">Apply Filters</v-btn>
      <v-btn color="error" @click="clearFilters()">Clear Filters</v-btn>
    </v-layout>

    <v-layout row wrap class="mt-2">
      <v-flex xs12 sm6 md4>
        <v-text-field
          label="Search For Address"
          v-model="full_address"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md2>
        <v-select
          :items="zipItems"
          v-model="zipSelected"
          box
          label="Zipcode"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field label="Latitude" v-model="latitude" box color="success" class="ml-1 mr-1"></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field label="Longitude" v-model="longitude" box color="success" class="ml-1 mr-1"></v-text-field>
      </v-flex>

      <!-- Second Row Start -->
      <v-flex xs12 sm6 md2>
        <v-select
          :items="recItems"
          v-model="recSelected"
          box
          label="Rec_Type"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field label="Search For Pin" v-model="pin" box color="success" class="ml-1 mr-1"></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md2>
        <v-select
          :items="ovaclsItems"
          v-model="ovaclsSelected"
          box
          label="OVACLS"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm6 md5>
        <v-select
          :items="class_descriptionItems"
          v-model="class_descriptionSelected"
          box
          label="Class Description"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <!-- Third Row -->
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min Current Land"
          v-model="minCurrentLand"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max Current Land"
          v-model="maxCurrentLand"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min Current Building"
          v-model="minCurrentBuilding"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max Current Building"
          v-model="maxCurrentBuilding"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min Current Total"
          v-model="minCurrentTotal"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max Current Total"
          v-model="maxCurrentTotal"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min Est. Market Value"
          v-model="minEstimatedMarketValue"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max Est. Market Value"
          v-model="maxEstimatedMarketValue"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
    </v-layout>
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
      full_address: "",
      latitude: "",
      longitude: "",
      zipItems: ["Any", "60613", "60614", "60615"],
      zipSelected: "",
      recItems: ["Any", "A-HD"],
      recSelected: "",
      pin: "",
      ovaclsItems: [
        "Any",
        "211",
        "212",
        "225",
        "297",
        "313",
        "314",
        "315",
        "318",
        "391",
        "396",
        "913",
        "915",
        "991",
        "996"
      ],
      ovaclsSelected: "",
      class_descriptionItems: [
        "Any",
        "Apartment buildings over three stories",
        "Mixed commercial/residential building, 6 units or less, sq ft less than 20,000",
        "Mixed use commercial/residential with apts. above seven units or more or building sq. ft. over 20,000",
        "Qualified single room occupancy improvements (must have cdu of sr)",
        "Rental mdrn row houses, 7 or more unts in a sing. dvlpment or 1 or more contig. prcls in comm. ownrshp",
        "Rented mdrn row houses, 7 or more units in a single develop. or 1 or more contig. parcels in cmn. ownshp.",
        "Special residential improvements",
        "Two or three story non-fireproof corridor apartments,or california type apartments, interior entrance",
        "Two or three story non-frprf. crt. and corridor apts or california type apts, no corridors, ex. entrance",
        "Two to Six Apartments, Over 62 Years",
        "2 or 3 story bldng, 7 or more units, sngle devel., 1 or more contig. parcels, in common ownership",
        "2 or 3 story building, 7 or more units, sgl. devel., one or more contig. parcels, in common ownership",
        "2 or 3 story non-frprf corridor apts, or california type apts, interior entrance"
      ],
      class_descriptionSelected: "",
      minCurrentLand: "",
      maxCurrentLand: "",
      minCurrentBuilding: "",
      maxCurrentBuilding: "",
      minCurrentTotal: "",
      maxCurrentTotal: "",
      minEstimatedMarketValue: "",
      maxEstimatedMarketValue: ""
    };
  },
  mounted() {
    // console.log(this.markers[0]);
    this.initMap();
  },
  methods: {
    clearFilters() {
      this.full_address = "";
      this.latitude = "";
      this.longitude = "";
      this.zipSelected = "";
      this.recSelected = "";
      this.pin = "";
      this.ovaclsSelected = "";
      this.class_descriptionSelected = "";
      this.minCurrentLand = "";
      this.maxCurrentLand = "";
      this.minCurrentBuilding = "";
      this.maxCurrentBuilding = "";
      this.minCurrentTotal = "";
      this.maxCurrentTotal = "";
      (this.minEstimatedMarketValue = ""), (this.maxEstimatedMarketValue = "");
    },
    applyFilters() {
      console.log(this.minEstimatedMarketValue);
      console.log(this.maxEstimatedMarketValue);
    },
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
