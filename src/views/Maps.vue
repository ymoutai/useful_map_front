<template>
  <v-app>
    <v-main>
      <h1>Map</h1>
      <MapsLoader
        :mapConfig="mapConfig"
        :apiKey="apiKey"
        @initialized="mapInitialized"
      />
    </v-main>
  </v-app>
</template>

<script>
import MapsLoader from "@/components/MapsLoader.vue";

export default {
  name: "Maps",

  data() {
    return {
      mapConfig: {
        center: {
          lat: 35.68944,
          lng: 139.69167,
        },
        zoom: 17,
      },
      apiKey: process.env.VUE_APP_GOOGLE_MAP_API,
    };
  },

  components: {
    MapsLoader,
  },

  methods: {
    mapInitialized: ({ api, map }) => {
      navigator.geolocation.getCurrentPosition((position) => {
        var latLng = new api.maps.LatLng(position.coords.latitude, position.coords.longitude, false);
        map.setCenter(latLng);

        const center = {
          lat: position.coords.latitude,
          lng: position.coords.longitude,
        };

        new api.maps.Marker({
          position: center,
          map: map
        });
      });
    },
  },
};
</script>
