<template>
  <div>
    <div class="top-details">
      <img class="user-picture" :src="user.avatar_url" alt="">
      <div class="user-infos">
        <span v-if="details.name"><strong>Name:</strong> {{ details.name }}</span>
        <span v-if="details.location"><strong>Location:</strong> {{ details.location }}</span>
        <span v-if="details.company"><strong>Company:</strong> {{ details.company }}</span>
        <span v-if="details.email"><strong>Company:</strong> {{ details.email }}</span>
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

