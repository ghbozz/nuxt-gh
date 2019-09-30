<template>
  <div class="column is-one-quarter">
    <div class="user-card">
      <div class="top-card" :style="'backgroundImage: url(' + user.avatar_url + ')'">
        <h3 class="user-name">{{ user.login }}</h3>
      </div>
      <div class="bottom-card">

      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: ['user']
  }
</script>

<style scoped>
  .user-card {
    width: 100%;
    height: 300px;
    border: 1px solid black;
  }

  .top-card {
    position: relative;
    height: 60%;
    background-size: cover;
    background-position: center;
  }

  .user-name {
    color: white;
    font-size: 1.5em;
    position: absolute;
    bottom: 5px;
    right: 5px;
  }
</style>
