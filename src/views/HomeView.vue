<template>
  <div class="home">
    <URLColorDisplay/>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import URLColorDisplay from '@/components/URLColorDisplay.vue' // @ is an alias to /src

export default defineComponent({
  name: 'HomeView',
  components: {
    URLColorDisplay
  }
})
</script>
