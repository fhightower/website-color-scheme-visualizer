<template>
  <div class="form" v-show="Object.keys(urlsColorData).length === 0">
    <form @submit.prevent="processURLs">
      <input type="text" placeholder="Enter comma-separated URLs here..." id="urls" v-model="urls">
      <input type="submit" @click="processURLs">
    </form>
  </div>

  <div v-for="(colorData, url, index) in urlsColorData" :key="url">
    <URLColorTreeMap :colorData="colorData" :url="url" :index="index"/>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
// import axios from 'axios'
import URLColorTreeMap from '@/components/URLColorTreeMap.vue'

const processingUrl = ''
const separator = ','
const maxUrls = 5

export default defineComponent({
  components: {
    URLColorTreeMap
  },
  data () {
    return {
      urls: '',
      urlsColorData: {}
    }
  },
  methods: {
    processURLs () {
      const splitUrls = this.urls.split(separator)
      if (splitUrls.length > maxUrls) {
        // todo: implement
        console.log('here!')
        return
      }

      // TODO: Update display to create unique ID for each url
      this.urlsColorData = {
        'https://liine.com': [
          {
            color: '#ffffff',
            value: 68.14450073242188
          },
          {
            color: '#8a2be2',
            value: 20.032840728759766
          },
          {
            color: '#191970',
            value: 5.0903120040893555
          },
          {
            color: '#dcdcdc',
            value: 3.7766830921173096
          },
          {
            color: '#c0c0c0',
            value: 0.9852216839790344
          },
          {
            color: '#dda0dd',
            value: 0.8210180401802063
          },
          {
            color: '#d8bfd8',
            value: 0.656814455986023
          },
          {
            color: '#e6e6fa',
            value: 0.4926108419895172
          }
        ],
        'https://art.hightower.space': [
          {
            color: '#ffffff',
            value: 70.9693374633789
          },
          {
            color: '#000000',
            value: 19.73293685913086
          },
          {
            color: '#c0c0c0',
            value: 2.6706230640411377
          },
          {
            color: '#696969',
            value: 2.2255191802978516
          },
          {
            color: '#808080',
            value: 1.829871416091919
          },
          {
            color: '#d8bfd8',
            value: 1.2363996505737305
          },
          {
            color: '#dcdcdc',
            value: 0.9396637082099915
          },
          {
            color: '#e6e6fa',
            value: 0.39564788341522217
          }
        ],
        'https://hightower.space': [
          {
            color: '#ffffff',
            value: 94.43270111083984
          },
          {
            color: '#dcdcdc',
            value: 2.5369977951049805
          },
          {
            color: '#c0c0c0',
            value: 2.1141648292541504
          },
          {
            color: '#808080',
            value: 0.9161381125450134
          }
        ]
      }

      /*
      axios.post(processingUrl, {
        urls: splitURLs
      })
        .then(function (response) {
          console.log(response)
          this.drawResults(response)
        })
        .catch(function (error) {
          console.error(error)
        })
      */
    }
  }
})
</script>
