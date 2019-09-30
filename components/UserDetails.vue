<template>
  <div class="user-details">
    <div class="top-details">
      <img class="user-picture" :src="user.avatar_url" alt="">
      <div v-if="details" class="user-infos">
        <span>Name: {{ details.name }}</span>
        <span>Website: {{ details.blog }}</span>
        <span>Location: {{ details.location }}</span>
        <span>Public Repos: {{ details.public_repos }}</span>
        <span>Followers: {{ details.followers }}</span>
        <span>Following: {{ details.following }}</span>
      </div>
    </div>
    <div class="bottom-details">
      <ul>
        <li class="lang" v-for="(key, value) in stats">{{ key }} / {{ value }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
  import { apiKey } from '~/env.js'
  import axios from 'axios'
  axios.defaults.headers.common['Authorization'] = `Bearer ${apiKey}`

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
            this.repos = res.data.map(repo => repo.name)
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
    font-size: 1.2em;
  }

  .top-details {
    margin-bottom: 64px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    width: 100%;
    color: rgb(255, 252, 242);
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
