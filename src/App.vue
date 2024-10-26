<script setup>
  import {ref, onMounted} from 'vue'
  import PocketBase from 'pocketbase'
  let db = new PocketBase("http://127.0.0.1:8090")
  let title = ref("")
  let description = ref("")

const submit = async ()=>{
  const data={
    title:title.value,
    description:description.value
  }
  await db.collection('posts').create(data)
}

</script>

<template>
  <label>
    <input class="px-4 py-4 bg-amber-300 hover:bg-yellow-300 rounded-lg border border blue mx-6 my-5 " v-model="title" placeholder="Title">
  </label>
  <label>
    <input class="px-4 py-4 bg-amber-300 hover:bg-yellow-300 rounded-lg border border blue m-6" v-model="description" placeholder="Description">
  </label>
  <button class="px-4 py-4 bg-zinc-200 hover:bg-zinc-600 rounded-full border border blue m-6 duration-200" @click="submit">SUBMIT</button>
</template>