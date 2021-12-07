<template>
  <div class="header">
    <h1>IP Address Tracker</h1>
    <br />
    <div class="search-bar">
      <input
        type="text"
        ref="searchIp"
        name="searchBox"
        placeholder="Search for any IP address or domain"
      />
      <div class="search" @click="getData">
        <img src="@/assets/right-arrow.png" alt="arrow image" />
      </div>
    </div>
  </div>
  <Map :location="location"> </Map>
  <Data :ipAddress="ipAddress" :location="location" :isp="isp"></Data>
</template>

<script>
require("dotenv").config();
import Map from "./components/Map.vue";
import Data from "./components/Data.vue";

export default {
  name: "App",
  components: { Map, Data },
  data() {
    return {
      ipAddress: "",
      location: null,
      timezone: null,
      isp: null,
      lat: null,
      lang: null,
    };
  },
  methods: {
    getData() {
      fetch(
        `https://geo.ipify.org/api/v2/country,city?apiKey=at_LhGWlEr8SRyWzGW8Nv8fd4uEvc2Tk&ipAddress=${this.$refs.searchIp.value}`
      )
        .then((res) => res.json())
        .then((data) => {
          this.ipAddress = data.ip;
          this.isp = data.isp;
          this.location = data.location;
        })
        .catch((err) => console.log(err));
    },
  },
  mounted() {
    this.getData();
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Lato:wght@300;400;700&display=swap");

body {
  background: url("D:/Study Material/view-engines/VUE/ip-address-tracker/src/assets/pattern-bg.png");
  background-position-x: center;
  background-repeat: no-repeat;
  background-size: cover;
}

#app {
  font-family: Rubik, Arial;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.header h1 {
  color: #fff;
  font-weight: 600;
}

.bgImg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
}

.search-bar {
  display: flex;
  justify-content: center;
  border-radius: 10px;
  overflow: hidden;
  margin: auto;
}

.search-bar input {
  width: 450px;
  padding: 15px;
  border: none;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
  font-size: 18px;
}

.search {
  background-color: black;
  padding: 5px;
  width: 50px;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
  cursor: pointer;
}

.search img {
  position: relative;
  top: 12px;
  height: 15px;
}
</style>
