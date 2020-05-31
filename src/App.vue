<template>
  <div class="container mx-auto" v-if="data">
    <h2>{{ data.title }}</h2>
    <img :src="data.hdurl" />
    {{data.explanation}}
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
