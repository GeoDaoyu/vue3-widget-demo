<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div id="viewDiv"></div>
  </div>
</template>

<script>
import EsriMap from '@arcgis/core/Map';
import MapView from '@arcgis/core/views/MapView';

export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  methods: {
    initMap() {
      const map = new EsriMap({
        basemap: 'topo-vector',
      });

      // eslint-disable-next-line no-unused-vars
      const view = new MapView({
        container: 'viewDiv',
        map,
      });
    },
  },
  mounted() {
    this.initMap();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://js.arcgis.com/4.19/@arcgis/core/assets/esri/css/main.css";
#viewDiv {
  height: 500px;
  width: 500px;
  margin: 0 auto;
}
</style>
