<template>
  <div>
    <div class="custom-container">
      <div class="left-scene">
        <app-user-details v-if="selectedUser" :user="selectedUser"></app-user-details>
      </div>
      <div class="right-scene">
        <input @change="search" class="search-bar" type="text" placeholder="search users on github" v-model="searchTerm">
        <div class="columns is-multiline is-mobile">
          <app-user-card v-for="user in searchResult" :user="user" @click.native="setUser(user)"></app-user-card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { apiKey } from '~/env.js'
import axios from 'axios'
axios.defaults.headers.common['Authorization'] = `Bearer ${apiKey}`

import Logo from '~/components/Logo.vue'
import UserCard from '~/components/UserCard.vue'
import UserDetails from '~/components/UserDetails.vue'

export default {
  data() {
    return {
      searchTerm: '',
      searchResult: [],
      selectedUser: null
    }
  },
  methods: {
    search() {
      if (this.searchTerm !== '') {
        return axios.get(`https://api.github.com/search/users?q=${this.searchTerm}`)
        .then((res) => {
          this.searchResult = res.data.items
        })
      }
    },
    setUser(user) {
      this.selectedUser = user;
    }
  },
  components: {
    appUserCard: UserCard,
    appUserDetails: UserDetails
  }
}
</script>

<style>
  .custom-container {
    width: 100vw;
    height: 100vh;
    display: flex;
  }

  .left-scene {
    position: fixed;
    padding: 40px;
    height: 100%;
    width: 40%;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    background-color: rgb(76, 126, 168);
  }

  .right-scene {
    overflow: scroll;
    position: absolute;
    top: 0;
    right: 0;
    padding: 40px;
    height: 100%;
    width: 60%;
    background-color: rgb(255, 252, 242);
    -webkit-box-shadow: inset -2px 2px 18px 0px rgba(0,0,0,0.2);
    -moz-box-shadow: inset -2px 2px 18px 0px rgba(0,0,0,0.2);
    box-shadow: inset -2px 2px 18px 0px rgba(0,0,0,0.2);
  }

  .search-bar {
    height: 64px;
    width: 100%;
    padding: 0px 15px;
    font-size: 28px;
    margin-bottom: 24px;
    border-radius: 50px;
    border: 1px solid rgba(30,30,30,0.1);
  }

  .search-bar:focus {
    outline: none;
  }
</style>
