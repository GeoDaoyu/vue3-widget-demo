<template>
  <div class="hello">
    <div id="viewDiv"></div>
    <MyZoom :view="view" v-if="ready"/>
  </div>
</template>

<script>
import EsriMap from '@arcgis/core/Map';
import MapView from '@arcgis/core/views/MapView';
import MyZoom from './MyZoom.vue';

export default {
  name: 'HelloWorld',
  view: null,
  data() {
    return {
      ready: false,
    };
  },
  components: {
    MyZoom,
  },
  methods: {
    initMap() {
      const map = new EsriMap({
        basemap: 'topo-vector',
      });

      this.view = new MapView({
        map,
        container: 'viewDiv',
      });
      this.view.when(() => {
        this.ready = true;
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
