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

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min Prior Land"
          v-model="minPriorLand"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max Prior Land"
          v-model="maxPriorLand"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min Prior Building"
          v-model="minPriorBuilding"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max Prior Building"
          v-model="maxPriorBuilding"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min Prior Total"
          v-model="minPriorTotal"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max Prior Total"
          v-model="maxPriorTotal"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min PPrior Land"
          v-model="minPPriorLand"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max PPrior Land"
          v-model="maxPPriorLand"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min PPrior Building"
          v-model="minPPriorBuilding"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max PPrior Building"
          v-model="maxPPriorBuilding"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min PPrior Total"
          v-model="minPPriorTotal"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max PPrior Total"
          v-model="maxPPriorTotal"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min PPrior Year"
          v-model="minPPriorYear"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max PPrior Year"
          v-model="maxPPriorYear"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm4 md2>
        <v-select
          :items="townItems"
          v-model="townSelected"
          box
          label="Town"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md2>
        <v-select
          :items="volumeItems"
          v-model="volumeSelected"
          box
          label="Volume"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md2>
        <v-select
          :items="locItems"
          v-model="locSelected"
          box
          label="Loc"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md2>
        <v-select
          :items="taxCodeItems"
          v-model="taxCodeSelected"
          box
          label="Tax Code"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md3>
        <v-select
          :items="neighborhoodItems"
          v-model="neighborhoodSelected"
          box
          label="Neighborhood"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md2>
        <v-text-field label="House #" v-model="houseNumber" box color="success" class="ml-1 mr-1"></v-text-field>
      </v-flex>

      <v-flex xs12 sm4 md2>
        <v-select
          :items="directionItems"
          v-model="directionSelected"
          box
          label="Direction"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md3>
        <v-select
          :items="streetItems"
          v-model="streetSelected"
          box
          label="Street"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md2>
        <v-select
          :items="suffixItems"
          v-model="suffixSelected"
          box
          label="Suffix"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md2>
        <v-select
          :items="aptItems"
          v-model="aptSelected"
          box
          label="Apt"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md2>
        <v-select
          :items="cityItems"
          v-model="citySelected"
          box
          label="City"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md3>
        <v-select
          :items="resTypeItems"
          v-model="resTypeSelected"
          box
          label="Res Type"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md3>
        <v-select
          :items="buildingUseItems"
          v-model="buildingUseSelected"
          box
          label="Building Use"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md2>
        <v-select
          :items="aptDescItems"
          v-model="aptDescSelected"
          box
          label="Apt Desc"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md2>
        <v-select
          :items="commUnitsItems"
          v-model="commUnitsSelected"
          box
          label="Comm Units"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md4>
        <v-select
          :items="extDescItems"
          v-model="extDescSelected"
          box
          label="Ext Desc"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md2>
        <v-select
          :items="fullBathItems"
          v-model="fullBathSelected"
          box
          label="Full Bath"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md2>
        <v-select
          :items="halfBathItems"
          v-model="halfBathSelected"
          box
          label="Half Bath"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md4>
        <v-select
          :items="bsmtDescItems"
          v-model="bsmtDescSelected"
          box
          label="BSMT Desc"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md4>
        <v-select
          :items="atticDescItems"
          v-model="atticDescSelected"
          box
          label="Attic Desc"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm4 md2>
        <v-select
          :items="acItems"
          v-model="acSelected"
          box
          label="AC"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm6 md2>
        <v-select
          :items="fireplaceItems"
          v-model="fireplaceSelected"
          box
          label="Fireplace"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm6 md4>
        <v-select
          :items="garDescItems"
          v-model="garDescSelected"
          box
          label="Garage Desc"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm6 md4>
        <v-text-field label="Min Age" v-model="minAge" box color="success" class="ml-1 mr-1"></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md4>
        <v-text-field label="Max Age" v-model="maxAge" box color="success" class="ml-1 mr-1"></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min Building Sq Ft"
          v-model="minBuildingSqFt"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max Building Sq Ft"
          v-model="maxBuildingSqFt"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min Land Sq Ft"
          v-model="minLandSqFt"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max Land Sq Ft"
          v-model="maxLandSqFt"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min Building SF"
          v-model="minBuildingSf"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max Building SF"
          v-model="maxBuildingSf"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min Units Total"
          v-model="minUnitsTotal"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max Units Total"
          v-model="maxUnitsTotal"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md2>
        <v-select
          :items="multiSaleItems"
          v-model="multiSaleSelected"
          box
          label="Multi Sale"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm6 md2>
        <v-select
          :items="deedTypeItems"
          v-model="deedTypeSelected"
          box
          label="Deed Type"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
      </v-flex>

      <v-flex xs12 sm6 md2>
        <v-text-field
          label="Sale Date xx/xx/xxxx"
          v-model="saleDate"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Min Sale Amount"
          v-model="minSaleAmount"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 sm6 md3>
        <v-text-field
          label="Max Sale Amount"
          v-model="maxSaleAmount"
          box
          color="success"
          class="ml-1 mr-1"
        ></v-text-field>
      </v-flex>

      <v-flex xs12 sm6 md2>
        <v-select
          :items="appcntItems"
          v-model="appcntSelected"
          box
          label="APPCNT"
          color="success"
          class="ml-1 mr-1"
        ></v-select>
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
      maxEstimatedMarketValue: "",
      minPriorLand: "",
      maxPriorLand: "",
      minPriorBuilding: "",
      maxPriorBuilding: "",
      minPriorTotal: "",
      maxPriorTotal: "",
      minPPriorLand: "",
      maxPPriorLand: "",
      minPPriorBuilding: "",
      maxPPriorBuilding: "",
      minPPriorTotal: "",
      maxPPriorTotal: "",
      minPPriorYear: "",
      maxPPriorYear: "",
      townItems: ["Any", "77"],
      townSelected: "",
      volumeItems: [
        "Any",
        "528",
        "532",
        "535",
        "536",
        "554",
        "557",
        "559",
        "582",
        "584",
        "586",
        "588",
        "590",
        "591",
        "592",
        "593",
        "594",
        "595",
        "596",
        "598",
        "599",
        "600"
      ],
      volumeSelected: "",
      locItems: ["Any", "City"],
      locSelected: "",
      taxCodeItems: [
        "Any",
        "77001",
        "77002",
        "77016",
        "77019",
        "77020",
        "77021",
        "77023",
        "77024",
        "77025",
        "77030",
        "77033",
        "77034",
        "77040",
        "77044",
        "77050",
        "77058",
        "77062",
        "77071"
      ],
      taxCodeSelected: "",
      neighborhoodItems: [
        "Any",
        "30",
        "52",
        "60",
        "103",
        "120",
        "131",
        "132",
        "141",
        "150"
      ],
      neighborhoodSelected: "",
      houseNumber: "",
      directionItems: ["Any", "N", "S", "W"],
      directionSelected: "",
      streetItems: [
        "Any",
        "16th",
        "17th",
        "18th",
        "19th",
        "21st",
        "Aberdeen",
        "Ada",
        "Albany",
        "Allport",
        "Artesian",
        "Ashland",
        "Bishop",
        "Blue Island",
        "Cambell",
        "Carpenter",
        "Cermak",
        "Claremont",
        "Cullerton",
        "Damen",
        "Division",
        "Erie",
        "Fillmore",
        "Flournoy",
        "Fullerton",
        "George",
        "Grand",
        "Grenshaw",
        "Haddon",
        "Harrison",
        "Hoyne",
        "Huron",
        "Jackson",
        "Justine",
        "Kedzie",
        "Laflin",
        "Lake",
        "Leavitt",
        "Lexington",
        "Loomis",
        "Lytle",
        "Maxwell",
        "May",
        "Miller",
        "Morgan",
        "Ohio",
        "Peoria",
        "Polk",
        "Race",
        "Racine",
        "Richmond",
        "Roosevelt",
        "Sacremento",
        "Superior",
        "Taylor",
        "Thomas",
        "Throop",
        "Troy",
        "Van Buren",
        "Vernon Park",
        "Washburne",
        "Washington",
        "Western",
        "Whipple",
        "Wood"
      ],
      streetSelected: "",
      suffixItems: ["Any", "Ave", "Blvd", "PL", "RD", "ST"],
      suffixSelected: "",
      aptItems: [
        "Any",
        "1",
        "2",
        "3",
        "4",
        "4609",
        "Rear",
        "1 2",
        "1 RR",
        "1FF",
        "1FL",
        "1R",
        "1st",
        "2FL",
        "2nd",
        "2RR",
        "2S",
        "3F",
        "3R",
        "BSMT",
        "C",
        "FF",
        "Front",
        "Gard",
        "HSE",
        "Rear"
      ],
      aptSelected: "",
      cityItems: ["Any", "Chicago"],
      citySelected: "",
      resTypeItems: [
        "Any",
        "1.5 - 1.9",
        "One Story",
        "Two Story",
        "Three Story"
      ],
      resTypeSelected: "",
      buildingUseItems: ["Any", "Single Family", "Multi Family"],
      buildingUseSelected: "",
      aptDescItems: ["Any", "2", "3", "4", "5", "6"],
      aptDescSelected: "",
      commUnitsItems: ["Any", "0", "1", "2", "3"],
      commUnitsSelected: "",
      extDescItems: ["Any", "Frame", "Frame/Masonry", "Masonry", "Stucco"],
      extDescSelected: "",
      fullBathItems: ["Any", "0", "1", "2", "3", "4", "5", "6", "7", "8", "9"],
      fullBathSelected: "",
      halfBathItems: ["Any", "0", "1", "2", "3", "4", "5", "6"],
      halfBathSelected: "",
      bsmtDescItems: [
        "Any",
        "Craw and Formal Rec. Room",
        "Full and Apartment",
        "Full and Formal Rec. Room",
        "Full and Unfinished",
        "Partial and Apartment",
        "Partial and Formal Rec. Room",
        "Partial and Unfinished",
        "Slab and Unfinished"
      ],
      bsmtDescSelected: "",
      atticDescItems: [
        "Any",
        "Full and Living Area",
        "None",
        "Partial and Living Area"
      ],
      atticDescSelected: "",
      acItems: ["Any", "0", "1", "2"],
      acSelected: "",
      fireplaceItems: ["Any", "0", "1", "2", "3", "4"],
      fireplaceSelected: "",
      garDescItems: [
        "Any",
        "1 1/2 Car Detached",
        "1 Car Attached",
        "2 1/2 Cars Detched",
        "2 Cars Attached",
        "2 Cars Detached",
        "3 1/2 Cars Detache",
        "3 Cars Attached",
        "3 Cars Detached",
        "4 Cars Attached",
        "4 Cars Detached"
      ],
      garDescSelected: "",
      minAge: "",
      maxAge: "",
      minBuildingSqFt: "",
      maxBuildingSqFt: "",
      minLandSqFt: "",
      maxLandSqFt: "",
      minBuildingSf: "",
      maxBuildingSf: "",
      minUnitsTotal: "",
      maxUnitsTotal: "",
      multiSaleItems: ["Any", "0", "1"],
      multiSaleSelected: "",
      deedTypeItems: ["Any", "0", "1", "2", "7"],
      deedTypeSelected: "",
      saleDate: "",
      minSaleAmount: "",
      maxSaleAmount: "",
      appcntItems: ["Any", "0", "1"],
      appcntSelected: ""
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
      this.minEstimatedMarketValue = "";
      this.maxEstimatedMarketValue = "";
      this.minPriorLand = "";
      this.maxPriorLand = "";
      this.minPriorBuilding = "";
      this.maxPriorBuilding = "";
      this.minPriorTotal = "";
      this.maxPriorTotal = "";
      this.minPPriorLand = "";
      this.maxPPriorLand = "";
      this.minPPriorBuilding = "";
      this.maxPPriorBuilding = "";
      this.minPPriorTotal = "";
      this.maxPPriorTotal = "";
      this.minPPriorYear = "";
      this.maxPPriorYear = "";
      this.townSelected = "";
      this.volumeSelected = "";
      this.locSelected = "";
      this.taxCodeSelected = "";
      this.neighborhoodSelected = "";
      this.houseNumber = "";
      this.directionSelected = "";
      this.streetSelected = "";
      this.suffixSelected = "";
      this.aptSelected = "";
      this.citySelected = "";
      this.resTypeSelected = "";
      this.buildingUseSelected = "";
      this.aptDescSelected = "";
      this.commUnitsSelected = "";
      this.extDescSelected = "";
      this.fullBathSelected = "";
      this.halfBathSelected = "";
      this.bsmtDescSelected = "";
      this.atticDescSelected = "";
      this.acSelected = "";
      this.fireplaceSelected = "";
      this.garDescSelected = "";
      this.minAge = "";
      this.maxAge = "";
      this.minBuildingSqFt = "";
      this.maxBuildingSqFt = "";
      this.minLandSqFt = "";
      this.maxLandSqFt = "";
      this.minBuildingSf = "";
      this.maxBuildingSf = "";
      this.minUnitsTotal = "";
      this.maxUnitsTotal = "";
      this.multiSaleSelected = "";
      this.deedTypeSelected = "";
      this.saleDate = "";
      this.minSaleAmount = "";
      this.maxSaleAmount = "";
      this.appcntSelected = "";
    },
    applyFilters() {
      // console.log(this.minSaleAmount);
      // console.log(this.maxSaleAmount);
      console.log(this.appcntSelected);
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
