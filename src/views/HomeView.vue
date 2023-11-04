<template>
  <div class="home">
    <URLCollector/>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import URLCollector from '@/components/URLCollector.vue' // @ is an alias to /src

export default defineComponent({
  name: 'HomeView',
  components: {
    URLCollector
  }
})
</script>
