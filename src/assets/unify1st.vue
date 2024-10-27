<script setup>
import { ref, onMounted } from 'vue'
import PocketBase from 'pocketbase'
let db = new PocketBase("http://127.0.0.1:8090")
let title = ref("")
let description = ref("")
let audioPlayer = ref(null)
let anthemPlayer = ref(null)
let anthemAudioUitm = ref(null)
let anthemAudioUm = ref(null)
let anthemAudioUpm = ref(null)
let source = ref('')
let url = ref('')
let isPlaying = ref(false)
let unis = [{
  name: 'UIAM',
  imgUrl: 'src/assets/uia.png',
  audioSrc: '/src/assets/leading the way uia.m4a'
},
{
  name: 'UITM',
  imgUrl: 'src/assets/uitm.png',
  audioSrc: '/src/assets/uitmdihatiku.m4a'
},
{
  name: 'UM',
  imgUrl: 'src/assets/um.png',
  audioSrc: '/src/assets/um.m4a'
},
{
  name: 'UPM',
  imgUrl: 'src/assets/upm.png',
  audioSrc: 'src/assets/Lagu Putra Gemilang  The UPM Anthem.mp3'
},
{
  name: 'UTM',
  imgUrl: 'src/assets/utm.png',
  audioSrc: 'src/assets/utm song.m4a'
}]

function playAudio(uni) {

  if(isPlaying.value){
    anthemPlayer.value.pause();
    isPlaying.value = false;
    return
  }

  if (audioPlayer.value) {
    anthemPlayer.value.src = uni.audioSrc
    anthemPlayer.value.play()
    isPlaying.value = true;
  } else {
    console.log(audioPlayer.value)
  }
}

function playAnthemUitm() {
  if (anthemAudioUitm.value) {
    anthemAudioUitm.value.play()
  } else {
    console.log(anthemAudioUitm.value)
  }
}

function playAnthemUia() {
  if (anthemAudioUia.value) {
    anthemAudioUia.value.play()
  } else {
    console.log(anthemAudioUia.value)
  }

}
const submit = async () => {
  const data = {
    title: title.value,
    description: description.value
  }
  await db.collection('posts').create(data)

  if (audioPlayer.value) {
    audioPlayer.value.play()
  } else {
    console.log(audioPlayer.value)
  }
}

</script>

<style>
/* Basic styling for the image */
.glow-image {

  /* Smooth transition for the glow effect */
}

/* Glow effect on hover */
.glow-image:hover {
  filter: drop-shadow(0 0 10px rgba(230, 255, 90, 0.7));
}

;

/* Glow effect on hover */
.glow-image:hover {
  filter: drop-shadow(0 0 10px rgba(230, 255, 90, 0.7));
}

body {
  background-color: rgb(40, 40, 40);
}
</style>

<template>
  <div class="w-full min-h-screen flex flex-col">
    <div class="mx-auto flex flex-col">
      <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ">
        <img src="./assets/unifywhite.png" alt="Description of the image" class="glow-image"
          style=" width: 160px; height: auto;" />
      </a>
      <h1 class="flex mx-auto" style="color: azure;">
        WANNA HERE A MASTERPIECE?
      </h1>
      <tr class="flex mx-auto">
        <th style="color: azure;">Click to listen to the anthem: </th>
      </tr>
      <br>



      <div className="flex mx-auto">
        <template v-for="uni, index in unis">
          <a>
            <img class="glow-image w-20 transition " @click="playAudio(uni)" :src='uni.imgUrl' />
          </a>
        </template>

        <!-- <a>
          <img src="./assets/uia.png" alt="Description of the image" @click="playAnthemUia" class="glow-image"
            style="border: none; width: 100px; height: auto;" />
        </a>
        <a href="https://uitm.edu.my/index.php/en/">
          <img src="./assets/uitm.png" alt="Description of the image" @click="playAnthemUitm" class="glow-image"
            style="border: none; width: 100px; height: auto;" />
        </a>
        <a href=" https://www.um.edu.my/">
          <img src="./assets/um.png" alt="Description of the image" class="glow-image"
            style="border: none; width: 100px; height: auto;" />
        </a>
        <a href=" https://www.upm.edu.my/">
          <img src="./assets/upm.png" alt="Description of the image" class="glow-image"
            style="border: none; width: 100px; height: auto;" />
        </a>
        <a href=" https://www.utm.my/">
          <img src="./assets/utm.png" alt="Description of the image" class="glow-image"
            style="border: none; width: 100px; height: auto;" />
        </a> -->

      </div>

  

      <form @submit="(e) => e.preventDefault()" class="my-5 mx-3">
        <label>
        <input class="px-4 py-4 bg-azure-300 hover:bg-yellow-300 rounded-lg border border blue mx-6 my-5 "
          v-model="title" placeholder="Name">
      </label>
      <label>
        <input class="px-4 py-4 bg-azure-300 hover:bg-yellow-300 rounded-lg border border blue m-6"
          v-model="description" placeholder="University">
      </label>
        <button class="px-4 py-4 bg-zinc-200 hover:bg-zinc-600 rounded-full border border blue m-6 duration-200"
          @click="submit">SUBMIT</button>
      </form>

      <audio ref="audioPlayer" >
        <source src="./assets/ding-sound-effect_1.mp3" type="audio/mpeg">
      </audio>

      <audio ref="anthemPlayer" >
        <source src="./assets/leading the way uia.m4a" type="audio/mpeg">
      </audio>

      <audio ref="anthemAudioUitm" >
        <source src="./assets/uitmdihatiku.m4a" type="audio/mpeg">
      </audio>
    </div>
  </div>

</template>
