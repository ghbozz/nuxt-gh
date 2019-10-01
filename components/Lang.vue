<template>
  <div class="bottom-details">
    <div class="columns is-mobile is-multiline">
      <div class="column is-half" v-for="(key, value) in stats" v-if="icons[value]">
        <div class="lang-card">
          <i :class="`devicon-${icons[value]}-plain colored`"></i>
          <div>
            <span class="lang-name"><strong>{{ value }}</strong></span>
            <br>
            <span class="lang-score">{{ key / 1000 }} <strong>KB</strong></span>
          </div>
        </div>
      </div>
    </div>
    <app-loader v-if="Object.keys(stats).length === 0"></app-loader>
  </div>
</template>

<script>
  import { icons } from '~/icons.js'
  import Loader from '~/components/Loader.vue'
  export default {
    data() {
      return {
        icons: icons
      }
    },
    props: ['stats'],
    components: {
      appLoader: Loader
    }
  }
</script>
