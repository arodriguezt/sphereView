<template>
  <div>
    <div id="viewer"></div>
    <q-dialog
      v-model="showNewMarkerDialog"
      style=""
      persistent
      full-width
      class="quantityDialog"
    >
      <div class="divDialog">
        <q-card>
          <q-card-section>
            <div class="text-h6 nomProducteDiv">Nuevo marcador</div>
          </q-card-section>

          <q-card-section class="q-pt-none quantityPriceInputs">
            <q-input
              ref="inputQuantityRef"
              v-model="idMarker"
              type="text"
              color="warning"
              dense
              autofocus
            ></q-input>
            <q-file
              v-model="selectedImage"
              label="Pick images"
              filled
              counter
              style="max-width: 300px"
              @input="onFileSelected"
            />
          </q-card-section>

          <q-card-actions align="left" class="text-primary">
            <q-btn
              v-close-popup
              flat
              class="cardActionButtonCancel"
              label="Cancelar"
            ></q-btn>
            <q-btn
              v-close-popup
              flat
              class="cardActionButtonConfirm"
              label="Aceptar"
              @click="addMarker(idMarker)"
            ></q-btn>
          </q-card-actions>
        </q-card>
      </div>
    </q-dialog>
  </div>
</template>

<script>
import { Viewer } from "@photo-sphere-viewer/core";
import { MarkersPlugin } from "@photo-sphere-viewer/markers-plugin";
import { onMounted, ref, reactive } from "vue";

export default {
  name: "IndexPage",
  //https://www.freepik.com/premium-photo/minsk-belarus-april-2019-full-seamless-hdri-panorama-360-angle-guestroom-with-sofa-tv-apartments-mansard-floor-vacation-house-equirectangular-spherical-projectionvr-content_28861885.htm#from_view=detail_alsolike
  setup() {
    const baseUrl = "https://photo-sphere-viewer-data.netlify.app/assets/";
    const imageLake =
      "https://images.unsplash.com/photo-1557971370-e7298ee473fb?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1760&q=80";
    const imagePlaya =
      "https://images.unsplash.com/photo-1563113794-ec21055a7b75?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2145&q=80";
    const imageSpace =
      "https://images.unsplash.com/photo-1594904578869-c011783103c7?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1285&q=80";

    let markers = {
      circle: [
        {
          id: "circle1",
          //yaw eix x de 0 a 6.24
          //pitch eix y de -1.5 a 1.5
          position: { yaw: 3, pitch: 0.5 },
          image: imageSpace,
          className: "imageMarker",
          tooltip: "A circle marker",
          anchor: "center center",
          size: {
            width: 187.5,
            height: 75,
          },
        },
        {
          id: "circle2",
          position: { yaw: 6.24, pitch: 0.1 },
          image: imagePlaya,
          className: "imageMarker",
          tooltip: "A circle marker",
          anchor: "center center",
          size: {
            width: 187.5,
            height: 75,
          },
        },
        {
          id: "circle3",
          className: "imageMarker",
          image: imageLake,
          position: { yaw: 2.2, pitch: 0.5 },
          tooltip: "A circle marker",
          anchor: "center center",
          size: {
            width: 187.5,
            height: 75,
          },
        },
        {
          id: "circle4",
          position: { yaw: 3.5, pitch: 0.4 },
          image: baseUrl + "sphere.jpg",
          className: "imageMarker",
          anchor: "bottom center",
          tooltip: "Click to open new panorama",
          size: {
            width: 187.5,
            height: 75,
          },
        },
      ],
      circle1: [
        {
          id: "circle",
          position: { yaw: 4.7, pitch: 0.5 },
          tooltip: "Faro",
          anchor: "center center",
          className: "imageMarker",
          image: baseUrl + "tour/key-biscayne-1.jpg",
          size: {
            width: 187.5,
            height: 75,
          },
        },
        {
          id: "circle2",
          position: { yaw: 6.24, pitch: 0.1 },
          image: imagePlaya,
          className: "imageMarker",
          tooltip: "A circle marker",
          anchor: "center center",
          size: {
            width: 187.5,
            height: 75,
          },
        },
        {
          id: "circle3",
          className: "imageMarker",
          image: imageLake,
          position: { yaw: 2.2, pitch: 0.5 },
          tooltip: "A circle marker",
          anchor: "center center",
          size: {
            width: 187.5,
            height: 75,
          },
        },
        {
          id: "circle4",
          position: { yaw: 3.5, pitch: 0.4 },
          image: baseUrl + "sphere.jpg",
          className: "imageMarker",
          anchor: "bottom center",
          tooltip: "Click to open new panorama",
          size: {
            width: 187.5,
            height: 75,
          },
        },
      ],
      circle2: [
        {
          id: "circle",
          position: { yaw: 6, pitch: 0.1 },
          tooltip: "Faro",
          anchor: "center center",
          className: "imageMarker",
          image: baseUrl + "tour/key-biscayne-1.jpg",
          size: {
            width: 187.5,
            height: 75,
          },
        },
        {
          id: "circle1",
          //yaw eix x de 0 a 6.24
          //pitch eix y de -1.5 a 1.5
          position: { yaw: 5.8, pitch: 0.1 },
          image: imageSpace,
          className: "imageMarker",
          tooltip: "A circle marker",
          anchor: "center center",
          size: {
            width: 187.5,
            height: 75,
          },
        },
        {
          id: "circle3",
          className: "imageMarker",
          image: imageLake,
          position: { yaw: 5.2, pitch: 0.1 },
          tooltip: "A circle marker",
          anchor: "center center",
          size: {
            width: 187.5,
            height: 75,
          },
        },
        {
          id: "circle4",
          position: { yaw: 4.8, pitch: 0.05 },
          image: baseUrl + "sphere.jpg",
          className: "imageMarker",
          anchor: "bottom center",
          tooltip: "Click to open new panorama",
          size: {
            width: 187.5,
            height: 75,
          },
        },
      ],
      circle3: [
        {
          id: "circle",
          position: { yaw: 4.7, pitch: 0.5 },
          tooltip: "Faro",
          anchor: "center center",
          className: "imageMarker",
          image: baseUrl + "tour/key-biscayne-1.jpg",
          size: {
            width: 187.5,
            height: 75,
          },
        },
        {
          id: "circle1",
          //yaw eix x de 0 a 6.24
          //pitch eix y de -1.5 a 1.5
          position: { yaw: 3, pitch: 0.5 },
          image: imageSpace,
          className: "imageMarker",
          tooltip: "A circle marker",
          anchor: "center center",
          size: {
            width: 187.5,
            height: 75,
          },
        },
        {
          id: "circle2",
          position: { yaw: 6.24, pitch: 0.1 },
          image: imagePlaya,
          className: "imageMarker",
          tooltip: "A circle marker",
          anchor: "center center",
          size: {
            width: 187.5,
            height: 75,
          },
        },
        {
          id: "circle4",
          position: { yaw: 3.5, pitch: 0.4 },
          image: baseUrl + "sphere.jpg",
          className: "imageMarker",
          anchor: "bottom center",
          tooltip: "Click to open new panorama",
          size: {
            width: 187.5,
            height: 75,
          },
        },
      ],
      circle4: [
        {
          id: "circle",
          position: { yaw: 4.5, pitch: 0.3 },
          tooltip: "Faro",
          anchor: "center center",
          className: "imageMarker",
          image: baseUrl + "tour/key-biscayne-1.jpg",
          size: {
            width: 187.5,
            height: 75,
          },
        },
        {
          id: "circle1",
          //yaw eix x de 0 a 6.24
          //pitch eix y de -1.5 a 1.5
          position: { yaw: 3, pitch: 0.5 },
          image: imageSpace,
          className: "imageMarker",
          tooltip: "A circle marker",
          anchor: "center center",
          size: {
            width: 187.5,
            height: 75,
          },
        },
        {
          id: "circle2",
          position: { yaw: 6.24, pitch: 0.1 },
          image: imagePlaya,
          className: "imageMarker",
          tooltip: "A circle marker",
          anchor: "center center",
          size: {
            width: 187.5,
            height: 75,
          },
          tooltip: {
            content: `
      <div>
        <p>Informació del marcador</p>
        <button id="my-button">Eliminar marcador</button>
      </div>
      </div>
    `,
            trigger: "hover",
          },
        },
        {
          id: "circle3",
          className: "imageMarker",
          image: imageLake,
          position: { yaw: 2.2, pitch: 0.5 },
          tooltip: "A circle marker",
          anchor: "center center",
          size: {
            width: 187.5,
            height: 75,
          },
        },
      ],
    };

    const idMarker = ref();
    const selectedImage = ref();
    const markerImageURL = ref();
    const actualMarker = ref("circle4");

    const markerPosition = reactive({ yaw: 0, pitch: 0 });
    const showNewMarkerDialog = ref(false);
    let viewer; // Variable per guardar el viewer

    // function getFilteredMarkers(markerId) {
    //   console.log(markerId);
    //   return markers.filter((marker) => marker.id !== markerId);
    // }

    function createMarker(id) {
      return {
        id: id,
        position: { yaw: markerPosition.yaw, pitch: markerPosition.pitch },
        image: markerImageURL.value,
        size: {
          width: 187.5,
          height: 75,
        },
        anchor: "bottom center",
        tooltip: "Generated pin on double click",
        data: {
          generated: true,
        },
        className: "imageMarker",
      };
    }

    function addMarker(id) {
      console.log(id);
      viewer.getPlugin(MarkersPlugin).addMarker(createMarker(id));
      markers[actualMarker.value].push(createMarker(id));
      console.log(markers);
    }

    function onFileSelected(event) {
      const file = event.target.files[0];
      markerImageURL.value = URL.createObjectURL(file);
    }

    onMounted(() => {
      viewer = new Viewer({
        container: "viewer",
        panorama: baseUrl + "sphere.jpg",
        loadingImg: baseUrl + "loader.gif",
        mousewheelCtrlKey: true,
        plugins: [
          [
            MarkersPlugin,
            {
              markers: markers[actualMarker.value],
            },
          ],
        ],
      });

      viewer.getPlugin(MarkersPlugin).addEventListener("select-marker", (e) => {
        // Recórrer la llista de marcadors
        for (let marker of markers[actualMarker.value]) {
          console.log(idMarker, marker.id);
          // Comprovar si l'identificador del marcador seleccionat coincideix amb el marcador actual
          if (e.marker.config.id === marker.id) {
            actualMarker.value = marker.id;
            // Actualitzar el panorama amb la imatge del marcador
            viewer.setPanorama(marker.image, {
              caption: marker.tooltip,
            });
            // Actualitzar la llista de marcadors per al nou panorama
            viewer.getPlugin(MarkersPlugin).setMarkers(markers[marker.id]);
            break;
          }
        }
      });

      viewer
        .getPlugin(MarkersPlugin)
        .addEventListener("marker-visibility", ({ marker, visible }) => {
          console.log(marker.config.id);
          const markerElement = document.getElementById(
            "psv-marker-" + marker.config.id
          );
          console.log(markerElement);

          if (visible) {
            // Aplica la clase pulsating-marker cuando el marcador es visible
            markerElement.classList.add("pulsating-marker");
          } else {
            // Quita la clase pulsating-marker cuando el marcador se oculta
            markerElement.classList.remove("pulsating-marker");
          }

          console.log(
            `Marker ${marker.id} is ${visible ? "visible" : "not visible"}`
          );
        });

      viewer.addEventListener("dblclick", ({ data }) => {
        showNewMarkerDialog.value = true;
        markerPosition.yaw = data.yaw;
        markerPosition.pitch = data.pitch;
      });
    });

    return {
      showNewMarkerDialog,
      idMarker,
      markerImageURL,
      selectedImage,

      addMarker,
      onFileSelected,
    };
  },
};
</script>
<style>
@keyframes pulse {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
  100% {
    transform: scale(1);
  }
}

/* Aplica la animación a la imagen del marcador */
.imageMarker {
  animation: pulse 1s 2;
}

html,
body,
#viewer {
  margin: 0;
  width: 100vw;
  height: 100vh;
  font-family: sans-serif;
}

.q-card {
  height: 38%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}
.quantityPriceInputs {
  align-self: center;
  width: 70%;
}
.cardActionButtonConfirm,
.cardActionButtonCancel {
  margin-left: 0px;
  position: relative;
  margin: auto;
}

.cardActionButtonCancel {
  color: #98033f !important;
}
.cardActionButtonConfirm {
  color: #268052 !important;
}
.priceSection {
  display: flex;
  justify-content: space-around;
  font-size: 1rem;
}
.nomProducteDiv {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/*S'han d'importar les clases externament*/
.psv-container {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  position: relative;
  background: radial-gradient(
    #fff 0,
    #fdfdfd 16%,
    #fbfbfb 33%,
    #f8f8f8 49%,
    #efefef 66%,
    #dfdfdf 82%,
    #bfbfbf 100%
  );
  overflow: hidden;
}
.psv-container * {
  box-sizing: content-box;
}
.psv-canvas-container {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 0;
  transition: opacity linear 0.1s;
}
.psv-canvas {
  display: block;
}
.psv-loader-container {
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 80;
}
.psv-loader {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  color: rgba(255, 255, 255, 0.7);
  width: 150px;
  height: 150px;
  outline: 3px solid transparent;
}
.psv-loader-canvas {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  color: rgba(61, 61, 61, 0.5);
  outline: 10px solid transparent;
  z-index: -1;
}
.psv-loader-text {
  font: 600 16px sans-serif;
}
.psv-navbar {
  display: flex;
  position: absolute;
  z-index: 90;
  bottom: -40px;
  left: 0;
  width: 100%;
  height: 40px;
  background: rgba(61, 61, 61, 0.5);
  transition: bottom ease-in-out 0.1s;
  font: 16px sans-serif;
}
.psv-navbar--open {
  bottom: 0;
}
.psv-navbar,
.psv-navbar * {
  box-sizing: content-box;
}
.psv-button {
  flex: 0 0 auto;
  padding: 10px;
  position: relative;
  cursor: pointer;
  height: 20px;
  width: 20px;
  background: 0 0;
  color: rgba(255, 255, 255, 0.7);
}
.psv-button--active {
  background: rgba(255, 255, 255, 0.2);
}
.psv-button--disabled {
  pointer-events: none;
  opacity: 0.5;
}
.psv-button-svg {
  width: 100%;
  transform: scale(1);
  transition: transform 0.2s ease;
  vertical-align: initial;
}
.psv-button:not(.psv-button--disabled):focus-visible {
  outline: 2px solid #007cff;
  outline-offset: -2px;
}
.psv-container:not(.psv--is-touch)
  .psv-button--hover-scale:not(.psv-button--disabled):hover
  .psv-button-svg {
  transform: scale(1.2);
}
.psv-move-button + .psv-move-button {
  margin-left: -10px;
}
.psv-custom-button {
  width: auto;
  min-width: 20px;
}
.psv-caption {
  flex: 1 1 100%;
  color: rgba(255, 255, 255, 0.7);
  overflow: hidden;
  text-align: center;
  cursor: default;
  padding: unset;
  height: unset;
  width: unset;
}
.psv-caption-content {
  display: inline-block;
  padding: 10px;
  white-space: nowrap;
}
.psv-zoom-range.psv-button {
  width: 80px;
  height: 1px;
  margin: 10px 0;
  padding: 9.5px 0;
  max-width: 600px;
}
.psv-zoom-range-line {
  position: relative;
  width: 80px;
  height: 1px;
  background: rgba(255, 255, 255, 0.7);
  transition: all 0.3s ease;
}
.psv-zoom-range-handle {
  position: absolute;
  border-radius: 50%;
  top: -3px;
  width: 7px;
  height: 7px;
  background: rgba(255, 255, 255, 0.7);
  transform: scale(1);
  transition: transform 0.3s ease;
}
.psv-zoom-range:not(.psv-button--disabled):hover .psv-zoom-range-line {
  box-shadow: 0 0 2px rgba(255, 255, 255, 0.7);
}
.psv-zoom-range:not(.psv-button--disabled):hover .psv-zoom-range-handle {
  transform: scale(1.3);
}
.psv-notification {
  position: absolute;
  z-index: 100;
  bottom: -40px;
  display: flex;
  justify-content: center;
  box-sizing: border-box;
  width: 100%;
  padding: 0 2em;
  opacity: 0;
  transition-property: opacity, bottom;
  transition-timing-function: ease-in-out;
  transition-duration: 0.2s;
}
.psv-notification-content {
  max-width: 50em;
  background: rgba(61, 61, 61, 0.8);
  border-radius: 4px;
  padding: 0.5em 1em;
  font: 14px sans-serif;
  color: #fff;
}
.psv-notification--visible {
  opacity: 100;
  bottom: 80px;
}
.psv-overlay {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: absolute;
  z-index: 110;
  inset: 0;
  background: radial-gradient(
    #fff 0,
    #fdfdfd 16%,
    #fbfbfb 33%,
    #f8f8f8 49%,
    #efefef 66%,
    #dfdfdf 82%,
    #bfbfbf 100%
  );
  opacity: 0.8;
}
.psv-overlay-image {
  margin-bottom: 4vh;
}
.psv-overlay-image svg {
  width: 50vw;
}
@media (orientation: landscape) {
  .psv-overlay-image svg {
    width: 25vw;
  }
}
.psv-overlay-title {
  color: #000;
  font: 30px sans-serif;
  text-align: center;
}
.psv-overlay-text {
  color: rgba(0, 0, 0, 0.8);
  font: 20px sans-serif;
  opacity: 0.8;
  text-align: center;
}
.psv-panel {
  position: absolute;
  z-index: 90;
  right: 0;
  height: 100%;
  width: 400px;
  max-width: calc(100% - 9px);
  background: rgba(10, 10, 10, 0.7);
  transform: translate3d(100%, 0, 0);
  opacity: 0;
  transition-property: opacity, transform;
  transition-timing-function: ease-in-out;
  transition-duration: 0.1s;
  cursor: default;
  margin-left: 9px;
}
.psv--has-navbar .psv-panel {
  height: calc(100% - 40px);
}
.psv-panel-close-button {
  display: none;
  position: absolute;
  top: -1px;
  right: 0;
  width: 19.2px;
  height: 19.2px;
  padding: 6.4px;
  background: 0 0;
  color: #fff;
  transition: background 0.3s ease-in-out;
  cursor: pointer;
}
.psv-panel-close-button svg {
  transition: transform 0.3s ease-in-out;
}
.psv-panel-close-button:hover {
  background: rgba(0, 0, 0, 0.9);
}
.psv-panel-close-button:hover svg {
  transform: scale(-1);
}
.psv-panel-resizer {
  display: none;
  position: absolute;
  top: 0;
  left: -9px;
  width: 9px;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.9);
  cursor: col-resize;
}
.psv-panel-resizer::before {
  content: "";
  position: absolute;
  top: 50%;
  left: 1px;
  margin-top: -14.5px;
  width: 1px;
  height: 1px;
  box-shadow: 1px 0 #fff, 3px 0 #fff, 5px 0 #fff, 1px 2px #fff, 3px 2px #fff,
    5px 2px #fff, 1px 4px #fff, 3px 4px #fff, 5px 4px #fff, 1px 6px #fff,
    3px 6px #fff, 5px 6px #fff, 1px 8px #fff, 3px 8px #fff, 5px 8px #fff,
    1px 10px #fff, 3px 10px #fff, 5px 10px #fff, 1px 12px #fff, 3px 12px #fff,
    5px 12px #fff, 1px 14px #fff, 3px 14px #fff, 5px 14px #fff, 1px 16px #fff,
    3px 16px #fff, 5px 16px #fff, 1px 18px #fff, 3px 18px #fff, 5px 18px #fff,
    1px 20px #fff, 3px 20px #fff, 5px 20px #fff, 1px 22px #fff, 3px 22px #fff,
    5px 22px #fff, 1px 24px #fff, 3px 24px #fff, 5px 24px #fff, 1px 26px #fff,
    3px 26px #fff, 5px 26px #fff, 1px 28px #fff, 3px 28px #fff, 5px 28px #fff;
  background: 0 0;
}
.psv-panel-content {
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  color: #dcdcdc;
  font: 16px sans-serif;
  overflow: auto;
}
.psv-panel-content:not(.psv-panel-content--no-margin) {
  padding: 1em;
}
.psv-panel-content--no-interaction {
  user-select: none;
  pointer-events: none;
}
.psv-panel--open {
  transform: translate3d(0, 0, 0);
  opacity: 1;
  transition-duration: 0.2s;
}
.psv-panel--open .psv-panel-close-button,
.psv-panel--open .psv-panel-resizer {
  display: block;
}
@media screen and (max-width: 400px) {
  .psv-panel {
    width: 100% !important;
    max-width: none;
  }
  .psv-panel-resizer {
    display: none !important;
  }
}
.psv-panel-menu {
  height: 100%;
  display: flex;
  flex-direction: column;
}
.psv-panel-menu-title {
  flex: none;
  display: flex;
  align-items: center;
  font: 24px sans-serif;
  margin: 24px 12px;
}
.psv-panel-menu-title svg {
  width: 24px;
  height: 24px;
  margin-right: 12px;
}
.psv-panel-menu-list {
  flex: 1;
  list-style: none;
  margin: 0;
  padding: 0;
  overflow-x: hidden;
}
.psv-panel-menu-item {
  min-height: 1.5em;
  padding: 0.5em 1em;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  transition: background 0.1s ease-in-out;
}
.psv-panel-menu-item--active {
  outline: 1px solid currentcolor;
  outline-offset: -1px;
}
.psv-panel-menu-item-icon {
  flex: none;
  height: 1.5em;
  width: 1.5em;
  margin-right: 0.5em;
}
.psv-panel-menu-item-icon img {
  max-width: 100%;
  max-height: 100%;
}
.psv-panel-menu-item-icon svg {
  width: 100%;
  height: 100%;
}
.psv-panel-menu-item:focus-visible {
  outline: 2px solid #007cff;
  outline-offset: -2px;
}
.psv-panel-menu--stripped .psv-panel-menu-item:hover {
  background: rgba(255, 255, 255, 0.2);
}
.psv-panel-menu--stripped .psv-panel-menu-item:nth-child(odd),
.psv-panel-menu--stripped .psv-panel-menu-item:nth-child(odd)::before {
  background: rgba(255, 255, 255, 0.1);
}
.psv-panel-menu--stripped .psv-panel-menu-item:nth-child(2n),
.psv-panel-menu--stripped .psv-panel-menu-item:nth-child(2n)::before {
  background: 0 0;
}
.psv-container:not(.psv--is-touch) .psv-panel-menu-item:hover {
  background: rgba(255, 255, 255, 0.2);
}
.psv-tooltip {
  position: absolute;
  z-index: 50;
  box-sizing: border-box;
  max-width: 187.5px;
  background: rgba(61, 61, 61, 0.8);
  border-radius: 4px;
  padding: 0.5em 1em;
  opacity: 0;
  transition-property: opacity, transform;
  transition-timing-function: ease-in-out;
  transition-duration: 0.1s;
}
.psv-tooltip-content {
  color: #fff;
  font: 14px sans-serif;
  text-shadow: 0 1px #000;
}
.psv-tooltip-arrow {
  position: absolute;
  height: 0;
  width: 0;
  border: 7px solid transparent;
}
.psv-tooltip--top-center,
.psv-tooltip--top-left,
.psv-tooltip--top-right {
  transform: translate3d(0, 5px, 0);
}
.psv-tooltip--top-center .psv-tooltip-arrow,
.psv-tooltip--top-left .psv-tooltip-arrow,
.psv-tooltip--top-right .psv-tooltip-arrow {
  border-top-color: rgba(61, 61, 61, 0.8);
}
.psv-tooltip--bottom-center,
.psv-tooltip--bottom-left,
.psv-tooltip--bottom-right {
  transform: translate3d(0, -5px, 0);
}
.psv-tooltip--bottom-center .psv-tooltip-arrow,
.psv-tooltip--bottom-left .psv-tooltip-arrow,
.psv-tooltip--bottom-right .psv-tooltip-arrow {
  border-bottom-color: rgba(61, 61, 61, 0.8);
}
.psv-tooltip--center-left,
.psv-tooltip--left-bottom,
.psv-tooltip--left-top {
  transform: translate3d(5px, 0, 0);
}
.psv-tooltip--center-left .psv-tooltip-arrow,
.psv-tooltip--left-bottom .psv-tooltip-arrow,
.psv-tooltip--left-top .psv-tooltip-arrow {
  border-left-color: rgba(61, 61, 61, 0.8);
}
.psv-tooltip--center-right,
.psv-tooltip--right-bottom,
.psv-tooltip--right-top {
  transform: translate3d(-5px, 0, 0);
}
.psv-tooltip--center-right .psv-tooltip-arrow,
.psv-tooltip--right-bottom .psv-tooltip-arrow,
.psv-tooltip--right-top .psv-tooltip-arrow {
  border-right-color: rgba(61, 61, 61, 0.8);
}
.psv-tooltip--left-top,
.psv-tooltip--top-left {
  box-shadow: -3px -3px 0 rgba(90, 90, 90, 0.7);
}
.psv-tooltip--top-center {
  box-shadow: 0 -3px 0 rgba(90, 90, 90, 0.7);
}
.psv-tooltip--right-top,
.psv-tooltip--top-right {
  box-shadow: 3px -3px 0 rgba(90, 90, 90, 0.7);
}
.psv-tooltip--bottom-left,
.psv-tooltip--left-bottom {
  box-shadow: -3px 3px 0 rgba(90, 90, 90, 0.7);
}
.psv-tooltip--bottom-center {
  box-shadow: 0 3px 0 rgba(90, 90, 90, 0.7);
}
.psv-tooltip--bottom-right,
.psv-tooltip--right-bottom {
  box-shadow: 3px 3px 0 rgba(90, 90, 90, 0.7);
}
.psv-tooltip--center-left {
  box-shadow: -3px 0 0 rgba(90, 90, 90, 0.7);
}
.psv-tooltip--center-right {
  box-shadow: 3px 0 0 rgba(90, 90, 90, 0.7);
}
.psv-tooltip--visible {
  transform: translate3d(0, 0, 0);
  opacity: 1;
  transition-duration: 0.1s;
}

/* src/style.scss */
.psv-markers {
  user-select: none;
  position: absolute;
  z-index: 10;
  width: 100%;
  height: 100%;
}
.psv-markers-svg-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 20;
}
.psv-marker {
  display: none;
}
.psv-marker--normal {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 30;
  overflow: visible;
  background-size: contain;
  background-repeat: no-repeat;
}
.psv-marker--transparent {
  display: block;
  opacity: 0;
}
.psv-marker--visible {
  display: block;
}
.psv-marker--has-tooltip,
.psv-marker--has-content {
  cursor: pointer;
}
.imageMarker {
  border-radius: 50%;
  border: 3px solid black;
  background-size: cover;
  width: 150px;
  height: 100px;
}
/*# sourceMappingURL=index.css.map */
</style>
