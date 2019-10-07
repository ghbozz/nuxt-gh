<template>
  <div v-if="details" class="user-details">
    <app-main-user-infos :details="details" :user="user"></app-main-user-infos>
    <app-lang v-if="done" :userStats="userStats" :forkedStats="forkedStats"></app-lang>
    <app-loader v-if="loading"></app-loader>
  </div>
</template>

<script>
  import { apiKey } from '~/env.js'
  import axios from 'axios'
  axios.defaults.headers.common['Authorization'] = `Bearer ${apiKey}`

  import MainUserInfos from '~/components/MainUserInfos.vue'
  import Lang from '~/components/Lang.vue'
  import Loader from '~/components/Loader.vue'

  export default {
    props: ['user'],
    data() {
      return {
        allRepos: [],
        userRepos: [],
        forkedRepos: [],
        userStats: {},
        forkedStats: {},
        details: null,
        done: false,
        loading: false
      }
    },
    methods: {
      getRepos() {
        this.resetData();
        this.loading = true
        return axios({
          method: "get",
          url: `https://api.github.com/users/${this.user.login}/repos`
          })
          .then(res => {
            // this.repos = this.repos.map(repo => repo.name)
            this.resetData();
            this.setRepos(res.data)
            this.getStats(this.userRepos, true)
            this.getStats(this.forkedRepos, false)
          })
      },
      setRepos(data) {
        this.forkedRepos = data.filter((item) => {
          return item.fork === true
        })
        this.userRepos = data.filter((item) => {
          return item.fork === false
        })
      },
      getStats(repos, owner) {
        const urls = repos.map(repo => `https://api.github.com/repos/${this.user.login}/${repo.name}/languages`)
        axios.all(urls.map(url => axios.get(url)))
          .then(axios.spread((...res) => {
            // all requests are now complete
            this.setStats(res.map(item => item.data), owner);
          }));
      },
      setStats(data, owner) {
        data.forEach((item) => {
          for (let [key, value] of Object.entries(item)) {
            if (owner) {
              this.userStats[key] ? this.userStats[key] += value : this.userStats[key] = value
            } else {
              this.forkedStats[key] ? this.forkedStats[key] += value : this.forkedStats[key] = value
            }
          }
        })
        this.loading = false
        this.done = true
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
        this.done = false;
        this.allRepos = {};
        this.userRepos = {};
        this.forkedRepos = {};
        this.userStats = {};
        this.forkedStats = {};
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
      appLang: Lang,
      appLoader: Loader
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
