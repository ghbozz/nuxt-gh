<template>
  <div>
    <div class="top-details">
      <img class="user-picture" :src="user.avatar_url" alt="">
      <div class="user-infos">
        <span v-if="details.name"><strong>Name:</strong> {{ details.name }}</span>
        <span v-if="details.location"><strong>Location:</strong> {{ details.location }}</span>
        <span v-if="details.company"><strong>Company:</strong> {{ details.company }}</span>
        <span v-if="details.email"><strong>Email:</strong> {{ details.email }}</span>
        <span v-if="details.blog"><strong>Website:</strong> {{ details.blog }}</span>
      </div>
      <a class="github-link" :href="'https://github.com/' + user.login" target="_blank"><i class="devicon-github-plain"></i></a>
    </div>
    <div class="socials-stats">
      <div class="columns">
        <div class="column">
          <div class="social-card">
            <span><strong>Public Repos</strong></span>
            <span>{{ details.public_repos }}</span>
          </div>
        </div>
        <div class="column">
          <div class="social-card">
            <strong>Followers</strong>
            <span>{{ details.followers }}</span>
          </div>
        </div>
        <div class="column">
          <div class="social-card">
            <strong>Following</strong>
            <span>{{ details.following }}</span>
          </div>
        </div>
        <div class="column">
          <div class="social-card">
            <strong>Public Gists</strong>
            <span>{{ details.public_gists }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: ['details', 'user']
  }
</script>

<style>
  .user-picture {
    width: 200px;
    margin-right: 10px;
    border-top-left-radius: 10px;
    border-bottom-left-radius: 10px;
  }

  .user-infos {
    display: flex;
    flex-direction: column;
    font-size: 1.1em;
    padding: 20px;
  }

  .top-details {
    position: relative;
    margin-bottom: 32px;
    display: flex;
    align-items: flex-start;
    justify-content: flex-start;
    width: 100%;
    background-color: rgb(255, 252, 242);
    color: black;
    border-radius: 10px;
    -webkit-box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
    -moz-box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
    box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
  }

  .socials-stats {
    margin-bottom: 32px;
  }

  .social-card {
    width: 100%;
    height: 75px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    background-color: rgb(255, 252, 242);
    border-radius: 10px;
    -webkit-box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
    -moz-box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
    box-shadow: 1px 2px 18px 0px rgba(0,0,0,0.2);
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

