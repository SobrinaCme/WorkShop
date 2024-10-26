<script setup>
import HelloWorld from './components/HelloWorld.vue'
import {ref, onMounted} from 'vue'

let prayerTimes = ref([])

onMounted(async function () {
  let response = await fetch("https://www.e-solat.gov.my/index.php?r=esolatApi/TakwimSolat&period=week&zone=WLY01")
  let data = await response.json()
  prayerTimes.value = data.prayerTime
})

// let count = ref(0);
// let word = ref("");
// function Increment() {
//   count.value += 1
// }

// function Decrement() {
//   count.value -= 1
// }
</script>

<template>
  <!-- <p>{{count}}</p>
  <button @click="Increment">Increment</button>
  <button @click="Decrement">Decrement</button> -->

<table>
  <thead>
    <tr>
      <th>Hijri</th>
      <th>Date</th>
      <th>Day</th>
      <th>Imsak</th>
      <th>Fajr</th>
      <th>Syuruk</th>
      <th>Dhur</th>
      <th>Asr</th>
      <th>Maghrib</th>
      <th>Isha</th>
    </tr>
    <tr v-for="prayerTime in prayerTimes">
      <th>{{ prayerTime.hijri }}</th>
      <th>{{ prayerTime.date }}</th>
      <th>{{ prayerTime.day }}</th>
      <th>{{ prayerTime.imsak }}</th>
      <th>{{ prayerTime.fajr }}</th>
      <th>{{ prayerTime.syuruk }}</th>
      <th>{{ prayerTime.dhuhr }}</th>
      <th>{{ prayerTime.asr }}</th>
      <th>{{ prayerTime.maghrib }}</th>
      <th>{{ prayerTime.isha }}</th>
    </tr>
  </thead>
</table>

</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
