<template>
  <div class="user-details">
    <div class="top-details">
      <img class="user-picture" :src="user.avatar_url" alt="">
      <div v-if="details" class="user-infos">
        <span v-if="details.name"><strong>Name:</strong> {{ details.name }}</span>
        <span v-if="details.location"><strong>Location:</strong> {{ details.location }}</span>
        <span v-if="details.blog"><strong>Website:</strong> {{ details.blog }}</span>
        <span><strong>Public Repos:</strong> {{ details.public_repos }}</span>
        <span><strong>Followers:</strong> {{ details.followers }}</span>
        <span><strong>Following:</strong> {{ details.following }}</span>
      </div>
      <a class="github-link" :href="'https://github.com/' + user.login" target="_blank"><i class="devicon-github-plain"></i></a>
    </div>
    <div class="bottom-details">
      <div class="columns is-mobile is-multiline" v-if="stats">
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
  </div>
</template>

<script>
  import { icons } from '~/icons.js'
  import { apiKey } from '~/env.js'
  import axios from 'axios'
  axios.defaults.headers.common['Authorization'] = `Bearer ${apiKey}`

  import Loader from '~/components/Loader.vue'

  export default {
    props: ['user'],
    data() {
      return {
        icons: icons,
        repos: [],
        stats: {},
        details: null
      }
    },
    methods: {
      getRepos() {
        this.resetData();
        return axios({
          method: "get",
          url: `https://api.github.com/users/${this.user.login}/repos`
          })
          .then(res => {
            this.repos = res.data.filter((item) => {
              return item.fork === false
            })
            this.repos = this.repos.map(repo => repo.name)
            this.getStats()
          })
      },
      getStats() {
        const urls = this.repos.map(repo => `https://api.github.com/repos/${this.user.login}/${repo}/languages`)
        axios.all(urls.map(url => axios.get(url)))
          .then(axios.spread((...res) => {
            // all requests are now complete
            this.setStats(res.map(item => item.data));
          }));
      },
      setStats(data) {
        this.stats = {};
        data.forEach((item) => {
          for (let [key, value] of Object.entries(item)) {
            if (this.stats[key]) {
              this.stats[key] += value
            } else {
              this.stats[key] = value
            }
          }
        })
      },
      getDetails() {
        return axios({
          method: "get",
          url: `https://api.github.com/users/${this.user.login}`
          })
          .then(res => {
            this.details = res.data
          })
      },
      resetData() {
        this.repos = {};
        this.stats = {};
      }
    },
    watch: {
      user() {
        this.getDetails();
        this.getRepos();
      }
    },
    created() {
      this.getDetails();
      this.getRepos();
    },
    components: {
      appLoader: Loader
    }
  }
</script>

<style scoped>
  .user-picture {
    width: 200px;
    margin-right: 40px;
  }

  .user-details {
    height: 100%;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    overflow: scroll;
  }

  .user-infos {
    display: flex;
    flex-direction: column;
    font-size: 1.1em;
  }

  .top-details {
    position: relative;
    margin-bottom: 64px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    width: 100%;
    background-color: rgb(255, 252, 242);
    color: black;
    border-radius: 10px;
    -webkit-box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
    -moz-box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
    box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
  }

  .bottom-details {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .user-picture {
    border-top-left-radius: 10px;
    border-bottom-left-radius: 10px;
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

  .github-link:link,
  .github-link:visited {
    position: absolute;
    bottom: 0px;
    right: 10px;
    font-size: 3em;
    color: rgb(77, 125, 168);
    transition: all .3s ease-out;
  }

  .github-link:hover {
    transform: scale(1.03);
  }

  .column {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
</style>
