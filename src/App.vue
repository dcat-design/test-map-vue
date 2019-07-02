<template>
  <div id="app">
    <Map :center="center" :points="points"/>
  </div>
</template>

<script>
import Map from './components/Map.vue';

export default {
  name: 'app',
  components: {
    Map,
  },
  data: () => ({
    center: [56.324285, 43.954825],
    points: [
      {
        id: '1',
        address:'Адрес номер 1',
        lat:'56.338995',
        lon:'43.909850',
      },
      {
        id: '2',
        address:'Адрес номер 2',
        lat:'56.328195',
        lon:'43.961298',
      },
      {
        id: '3',
        address:'Адрес номер 3',
        lat:'56.335088',
        lon:'43.937985',
      },
    ],
  })
}
</script>

