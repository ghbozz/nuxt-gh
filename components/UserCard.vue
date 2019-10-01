<template>
  <div class="column is-one-quarter">
    <div class="user-card">
      <div class="top-card" :style="'backgroundImage: url(' + user.avatar_url + ')'">
        <h3 class="user-name">{{ user.login }}</h3>
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
    cursor: pointer;
    width: 100%;
    height: 200px;
    border-radius: 10px;
    -webkit-box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
    -moz-box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
    box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
    transition: all .3s ease-out;
  }

  .user-card:hover {
    transform: translateY(-5px);
    -webkit-box-shadow: 1px 15px 18px 0px rgba(0,0,0,0.2);
    -moz-box-shadow: 1px 15px 18px 0px rgba(0,0,0,0.2);
    box-shadow: 1px 15px 18px 0px rgba(0,0,0,0.2);
  }

  .top-card {
    position: relative;
    height: 100%;
    background-size: cover;
    background-position: center;
    border-radius: 10px;
  }

  .top-card h3 {
    position: absolute;
    right: 0;
    bottom: 15px;
    padding: 5px 10px;
    text-align: right;
    font-weight: 700;
    width: 100%;
    background-color: rgba(20, 20, 20, 0.8);
  }

  .user-name {
    color: white;
    font-size: 1.2em;
    position: absolute;
    bottom: 5px;
    right: 5px;
  }
</style>
