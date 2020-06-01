<template>
  <div class="bg-gray-800 min-h-screen">
    <div class="container flex mx-auto p-4 flex-col lg:flex-row" v-if="data">
      <div class="w-full lg:w-9/12 p-4">
        <h2 class="mb-4 text-center text-gray-300 text-2xl font-bold">{{ data.title }}</h2>
        <img id="nasa-image" class="mx-auto object-cover" :src="data.hdurl" />
      </div>
      <div class="w-full lg:w-3/12 inline-block">
        <div class="bg-gray-900 p-4 rounded md:mt-16">
          <h3 class="text-2xl text-gray-300 font-bold border-b border-gray-200 mb-2">Description</h3>
          <span class="italic text-gray-300">{{data.explanation}}</span>
        </div>
      </div>
    </div>
  </div>
</template>
 
<script lang="ts">
import { defineComponent, ref, onMounted } from "vue"

export default defineComponent({
  name: "App",
  components: {},

  setup() {
    const url = `https://api.nasa.gov/planetary/apod?api_key=${process.env.API_KEY}`

    const data = ref({})
    onMounted(() => {
      fetch(url)
        .then(stream => stream.json())
        .then(resp => {
          data.value = resp
        })
    })

    return {
      data
    }
  }
})
</script>

<style scoped>
#nasa-image {
  max-height: 820px;
}
</style>