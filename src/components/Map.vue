<template>
  <yandex-map
    class="Map"
    :settings="settings"
    :coords="center"
    zoom="12"
  >
    <ymap-marker
      v-for="point in pointsList"
      :key="point.id"
      :marker-id="point.id"
      :coords="point.coords"
      :hint-content="point.comment"
      :balloon="getBaloon(point)"
      marker-type="Placemark"
    />
  </yandex-map>
</template>

<script>
import { yandexMap, ymapMarker } from 'vue-yandex-maps'

export default {
  components: {
    yandexMap,
    ymapMarker
  },
  props: {
    points: Array,
    center: {
      type: Array,
      required: true,
    }
  },
  data: () => ({
    settings: {
      apiKey: '292a1fb2-2d7b-4735-a4e9-d42c7db4f9e3',
      lang: 'ru_RU',
      coordorder: 'latlong',
      version: '2.1',
    },
  }),
  computed: {
    pointsList() {
      return this.points.reduce((arr, el) => {
        const {id, address, lat, lon} = el;
        const comment = `
          Task name: <strong>${id}</strong><br/>
          Address: <strong>${address}</strong>
        `;
        const point = {
          id,
          address,
          comment,
          coords: [ lat, lon ],
        };
        return [...arr, point];
      }, []);
    },
    
  },
  methods: {
    getBaloon({id, address}) {
      return {
        header: `Task name: <strong>${id}</strong>`,
        body: `Address: <strong>${address}</strong>`
      }
    }
  }
}
</script>

<style>
.Map {
  width: calc(100vw - 40px);
  height: calc(100vh - 40px);
}
</style>