<script setup>
import {ref, onMounted} from "vue"
let prayerTimes = ref([])

onMounted( async function(){

    let response = await fetch("https://www.e-solat.gov.my/index.php?r=esolatApi/TakwimSolat&period=today&zone=SBH06")
    let data = await  response.json()
    prayerTimes.value = data.prayerTime
    console.log(data.prayerTime)
})
</script>

<template>

<table>
  <thead>
    <tr>
      <th>Hijri</th>
      <th>Fajr</th>
      <th>Dhuhr</th>
      <th>Asr</th>
      <th>Maghrib</th>
      <th>Isha</th>
    </tr>
  </thead>
</table>

  <div v-for="time in prayerTimes">
    <p class="text-xl">{{ time.imsak }}</p>
    <p class="text-xl">{{ time.fajr }}</p>
    <p class="text-xl">{{ time.dhuhr }}</p>
    <p class="text-xl">{{ time.asr }}</p>
    <p class="text-xl">{{ time.maghrib }}</p>
    <p class="text-xl">{{ time.isha }}</p>
  </div>

</template>