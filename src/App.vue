<script setup>
  import {ref, onMounted} from 'vue'
  import PocketBase from 'pocketbase'
  let db = new PocketBase("http://127.0.0.1:8090")
  let title = ref("")
  let description = ref("")
  let audioPlayer = ref(null)
  let anthemAudioUia = ref(null)
  let anthemAudioUitm = ref(null)
  let anthemAudioUm = ref(null)
  let anthemAudioUpm = ref(null)

  function playAnthemUitm(){
    if(anthemAudioUitm.value){
      anthemAudioUitm.value.play()
  }else{
    console.log(anthemAudioUitm.value)
  }}

  function playAnthemUia(){
    if(anthemAudioUia.value){
      anthemAudioUia.value.play()
  }else{
    console.log(anthemAudioUia.value)
  }

  }
const submit = async ()=>{
  const data={
    title:title.value,
    description:description.value
  }
  await db.collection('posts').create(data)

  if(audioPlayer.value){
    audioPlayer.value.play()
  }else{
    console.log(audioPlayer.value)
  }
}
  
</script>

<style>
    /* Basic styling for the image */
    .glow-image {
      width: auto;
      height: auto;
      transition: filter 0.3s ease ; /* Smooth transition for the glow effect */
    }

    /* Glow effect on hover */
    .glow-image:hover {
      filter : drop-shadow(0 0 10px rgba(21, 0, 255, 0.7));
    }
     body {
        background-color: rgb(219, 219, 219);
    }
  
</style>

<template>
  <h>
    ARE YOU NEW STUDENT?
  </h>
  <tr>
    <th>Visit us: </th>
  </tr>

<a href="https://uitm.edu.my/index.php/en/">
  <img src="./assets/unify.png" alt="Description of the image" class="glow-image" style=" width: 160px; height: auto;" />
</a>

  <div className="flex">
  <a>
  <img src="./assets/uia.png" alt="Description of the image" @click="playAnthemUia" class="glow-image" style="border: none; width: 100px; height: auto;" />

</a>
<a href="https://uitm.edu.my/index.php/en/">
  <img src="./assets/uitm.png" alt="Description of the image" @click="playAnthemUitm" class="glow-image" style="border: none; width: 100px; height: auto;" />
</a>
<a href=" https://www.um.edu.my/">
  <img src="./assets/um.png" alt="Description of the image" class="glow-image" style="border: none; width: 100px; height: auto;" />
</a>
<a href=" https://www.upm.edu.my/">
  <img src="./assets/upm.png" alt="Description of the image" class="glow-image" style="border: none; width: 100px; height: auto;" />
</a>
<a href=" https://www.utm.my/">
  <img src="./assets/utm.png" alt="Description of the image" class="glow-image" style="border: none; width: 100px; height: auto;" />
</a>

</div>

  <label>
    <input class="px-4 py-4 bg-amber-300 hover:bg-yellow-300 rounded-lg border border blue mx-6 my-5 " v-model="title" placeholder="Name">
  </label>
  <label>
    <input class="px-4 py-4 bg-amber-300 hover:bg-yellow-300 rounded-lg border border blue m-6" v-model="description" placeholder="University">
  </label>
  
  <form @submit="(e)=>e.preventDefault()" class="my-5 mx-3">
   <button class="px-4 py-4 bg-zinc-200 hover:bg-zinc-600 rounded-full border border blue m-6 duration-200" @click="submit">SUBMIT</button>
  </form>

<audio ref="audioPlayer" controls>
        <source src="./assets/ding-sound-effect_1.mp3" type="audio/mpeg">
</audio>

<audio ref="anthemAudioUia" controls>
        <source src="./assets/leading the way uia.m4a" type="audio/mpeg">
</audio>

<audio ref="anthemAudioUitm" controls>
        <source src="./assets/uitmdihatiku.m4a" type="audio/mpeg">
</audio>

</template>

