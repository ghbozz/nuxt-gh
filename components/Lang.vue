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

<style>
  .bottom-details {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .lang-card {
    background-color: rgb(255, 252, 242);
    padding: 20px;
    width: 100%;
    height: 150px;
    display: flex;
    align-items: center;
    border-radius: 10px;
    -webkit-box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
    -moz-box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
    box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
  }

  .lang-card i {
    font-size: 4em;
    margin-right: 20px;
  }

  .lang {
    color: rgb(255, 252, 242);
    font-size: 1.2em;
  }

  .column {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
</style>
