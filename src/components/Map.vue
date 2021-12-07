<template>
  <div id="mapContainer"></div>
</template>

<script>
mapboxgl.accessToken =
  "pk.eyJ1IjoibWF5YW5rLWo2MTkiLCJhIjoiY2t0bjY3cWs0MDJiNzJwdGluZ29veW83OCJ9.ILceh4WZaH1WomhH_ZBAUw";

export default {
  props: ["location"],
  data() {
    return {
      mapData: null,
    };
  },
  methods: {
    renderMap() {
      const mapViewData = {
        container: "mapContainer",
        style: "mapbox://styles/mapbox/streets-v11",
        center: [0, 0],
        zoom: 2,
        pitch: 36,
        hash: true,
      };

      const map = new mapboxgl.Map(mapViewData);

      map.addControl(new mapboxgl.NavigationControl());

      this.mapData = map;
    },

    flyToLocation(data) {
      if (data != null) {
        new mapboxgl.Marker({ color: "black", scale: "2" })
          .setLngLat({ lng: data.lng, lat: data.lat })
          .addTo(this.mapData);

        this.mapData.flyTo({
          center: [data.lng, data.lat],
          zoom: 12,
          speed: 1.6,
          curve: 1,
          easing(t) {
            return t;
          },
        });
      }
    },
  },

  mounted() {
    this.renderMap();
  },
  updated() {
    this.flyToLocation(this.location);
  },
};
</script>

<style>
#mapContainer {
  position: absolute;
  top: 265px;
  height: 65%;
  width: 100%;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
</style>
