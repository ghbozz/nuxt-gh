<template>
  <div v-if="details" class="user-details">
    <app-main-user-infos :details="details" :user="user"></app-main-user-infos>
    <app-lang v-if="stats" :stats="stats"></app-lang>
  </div>
</template>

<script>
  import { apiKey } from '~/env.js'
  import axios from 'axios'
  axios.defaults.headers.common['Authorization'] = `Bearer ${apiKey}`

  import MainUserInfos from '~/components/MainUserInfos.vue'
  import Lang from '~/components/Lang.vue'

  export default {
    props: ['user'],
    data() {
      return {
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
            // if (this.stats[key]) {
            //   this.stats[key] += value
            // } else {
            //   this.stats[key] = value
            // }
            this.stats[key] ? this.stats[key] += value : this.stats[key] = value
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
      appMainUserInfos: MainUserInfos,
      appLang: Lang
    }
  }
</script>

<style>
  .user-details {
    height: 100%;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    overflow: scroll;
  }
</style>
