<template>
  <div class="bottom-details">
    <div class="select-buttons">
      <div class="columns">
        <div class="column">
          <div class="select-btn" :class="{ active: forked }" @click="forked = false"><strong>User Repositories</strong></div>
        </div>
        <div class="column">
          <div class="select-btn" :class="{ active: !forked }" @click="forked = true"><strong>Forked Repositories</strong></div>
        </div>
      </div>
    </div>

    <div class="columns is-multiline" v-if="!forked">
      <div class="column is-half" v-for="(key, value) in userStats" v-if="icons[value]">
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

    <div class="columns is-multiline" v-if="forked">
      <div class="column is-half" v-for="(key, value) in forkedStats" v-if="icons[value]">
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
    <!-- <app-loader v-if="Object.keys(userStats).length === 0"></app-loader> -->
  </div>
</template>

<script>
  import { icons } from '~/icons.js'
  import Loader from '~/components/Loader.vue'
  export default {
    data() {
      return {
        icons: icons,
        forked: false
      }
    },
    props: ['userStats', 'forkedStats'],
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
    flex-direction: column;
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

  .select-buttons {
    margin-bottom: 24px;
    width: 100%;
  }

  .select-btn {
    cursor: pointer;
    background-color: rgb(255, 252, 242);
    padding: 20px;
    width: 100%;
    height: 75px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 10px;
    -webkit-box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
    -moz-box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
    box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
    transition: all .3s ease-out;
  }

  .select-btn:hover {
    transform: translateY(-5px);
    background-color: rgb(255, 252, 242);
  }

  .select-btn:active {
    transform: translateY(0px);
  }

  .active {
    background-color: rgb(200, 200, 200);
  }

  .column {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
</style>
