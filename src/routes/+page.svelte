<script lang="ts">
  import L from 'leaflet';
  const gent = new L.LatLng(51.043, 3.718);
  let latlng = gent;
  let map;
  function setupMap(container: HTMLElement) {
    map = L.map(container).setView(gent, 13);
    L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 19,
        attribution: '© <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);
    map.on('mousemove', (e) => {
      latlng = e.latlng
    })
  }
</script>

<div id="map" use:setupMap></div>
<div id="overlay">{latlng.toString()}</div>

<style>
  @import 'leaflet/dist/leaflet.css';
  :global(body) { margin: 0px; }
  #map { height: 100vh; }
  #overlay {
    position: absolute;
    bottom: 0.2em;
    left: 0.2em;
    background: white;
    border: 1px solid black;
    font-size: large;
    padding: 0.2em;
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    z-index: 400;  /* leaflet is somewhere at 300, it seems */
  }
</style>
