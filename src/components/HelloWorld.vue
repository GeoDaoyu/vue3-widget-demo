<template>
  <div class="hello">
    <div id="viewDiv"></div>
    <div class="widgets">
      <div id="zoom"></div>
      <div id="zoom-wm">
        <div class="esri-component esri-zoom esri-widget">
          <div
            class="esri-widget--button esri-widget esri-interactive"
            role="button"
            tabindex="0"
            title="放大"
            v-on:click="zoomIn"
          >
            <span
              aria-hidden="true"
              role="presentation"
              class="esri-icon esri-icon-plus"
            >
            </span>
            <span class="esri-icon-font-fallback-text">放大</span>
          </div>
          <div
            class="esri-widget--button esri-widget esri-interactive"
            role="button"
            tabindex="-1"
            title="缩小"
            v-on:click="zoomOut"
          >
            <span
              aria-hidden="true"
              role="presentation"
              class="esri-icon esri-icon-minus"
            >
            </span>
            <span class="esri-icon-font-fallback-text">缩小</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import EsriMap from '@arcgis/core/Map';
import MapView from '@arcgis/core/views/MapView';
import Zoom from '@arcgis/core/widgets/Zoom';
import ZoomViewModel from '@arcgis/core/widgets/Zoom/ZoomViewModel';

export default {
  name: 'HelloWorld',
  zoomVM: null,
  methods: {
    initMap() {
      const map = new EsriMap({
        basemap: 'topo-vector',
      });

      const view = new MapView({
        map,
        container: 'viewDiv',
      });

      view.when((currView) => {
        this.addZoomByWidget(currView);
        this.addZoomByVM(currView);
      });
    },
    addZoomByWidget(view) {
      // eslint-disable-next-line no-unused-vars
      const zoom = new Zoom({
        view,
        container: 'zoom',
      });
    },
    addZoomByVM(view) {
      this.zoomVM = new ZoomViewModel({
        view,
      });
    },
    zoomIn() {
      this.zoomVM.zoomIn();
    },
    zoomOut() {
      this.zoomVM.zoomOut();
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
.widgets {
  position: absolute;
  border: 1px black solid;
  top: 60px;
  left: 100px;
  height: 500px;
  width: 100px;
}
</style>
