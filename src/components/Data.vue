<template>
  <div class="dataBlock">
    <div class="dataCards">
      <h3>IP ADDRESS</h3>
      <h2>{{ ipAddress }}</h2>
    </div>
    <hr width="2" size="80" />
    <div class="dataCards">
      <h3>LOCATION</h3>
      <h2>{{ fullAddress }}</h2>
    </div>
    <hr width="2" size="80" />
    <div class="dataCards">
      <h3>TIMEZONE</h3>
      <h2>{{ timezone }}</h2>
    </div>
    <hr width="2" size="80" />
    <div class="dataCards">
      <h3>ISP</h3>
      <h2>{{ isp }}</h2>
    </div>
  </div>
</template>

<script>
export default {
  props: ["ipAddress", "location", "isp"],
  data() {
    return {
      country: null,
      region: null,
      city: null,
      fullAddress: null,
      timezone: null,
    };
  },
  methods: {},
  updated() {
    this.country = this.location.country;
    this.region = this.location.region;
    this.city = this.location.city;
    this.fullAddress = `${this.city}, ${this.region}, ${this.country}`;
    this.timezone = this.location.timezone;
  },
};
</script>

<style>
.dataBlock {
  position: relative;
  display: flex;
  justify-content: space-around;
  padding: 20px;
  top: 40px;
  background-color: #fff;
  width: 90%;
  height: 120px;
  border-radius: 15px;
  margin: 0 auto;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.dataBlock hr {
  color: black;
}

.dataCards {
  padding: 10px;
  text-align: left;
}

.dataCards h3 {
  opacity: 0.5;
  font-weight: 700;
  font-size: 15px;
}

.dataCards h2 {
  margin-top: 5px;
  font-weight: 600;
}
</style>
