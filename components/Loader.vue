<template>
  <div style="margin-top: 60px; position: relative;">
    <i class="devicon-github-plain github-logo"></i>
    <div class='loader loader1'>
      <div>
        <div>
          <!-- <div> -->
            <!-- <div> -->
              <!-- <div> -->
                <!-- <div></div> -->
              <!-- </div> -->
            <!-- </div> -->
          <!-- </div> -->
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .github-logo {
    z-index: 10;
    position: absolute;
    transform: translate(-50%, -50%);
    top: 50%;
    left: 50%;
    font-size: 6.5em;
    color: rgb(255, 252, 242);
  }

  @-webkit-keyframes rotate {
    0% {
      -webkit-transform: rotate(0deg);
              transform: rotate(0deg);
    }
    50% {
      -webkit-transform: rotate(180deg);
              transform: rotate(180deg);
    }
    100% {
      -webkit-transform: rotate(360deg);
              transform: rotate(360deg);
    }
  }
  @keyframes rotate {
    0% {
      -webkit-transform: rotate(0deg);
              transform: rotate(0deg);
    }
    50% {
      -webkit-transform: rotate(180deg);
              transform: rotate(180deg);
    }
    100% {
      -webkit-transform: rotate(360deg);
              transform: rotate(360deg);
    }
  }
  @-webkit-keyframes rotate2 {
    0% {
      -webkit-transform: rotate(0deg);
              transform: rotate(0deg);
      border-top-color: rgb(255, 252, 242);
    }
    50% {
      -webkit-transform: rotate(180deg);
              transform: rotate(180deg);
      border-top-color: rgb(65, 184, 131);
    }
    100% {
      -webkit-transform: rotate(360deg);
              transform: rotate(360deg);
      border-top-color: rgb(255, 252, 242);
    }
  }
  @keyframes rotate2 {
    0% {
      -webkit-transform: rotate(0deg);
              transform: rotate(0deg);
      border-top-color: rgb(255, 252, 242);
    }
    50% {
      -webkit-transform: rotate(180deg);
              transform: rotate(180deg);
      border-top-color: rgb(65, 184, 131);
    }
    100% {
      -webkit-transform: rotate(360deg);
              transform: rotate(360deg);
      border-top-color: rgb(255, 252, 242);
    }
  }
  * {
    box-sizing: border-box;
  }

  body {
    background: #f9f9f9;
    padding-bottom: 100px;
  }

  h1, h3 {
    display: block;
    margin: 0px auto;
    text-align: center;
    font-family: 'Tahoma';
    font-weight: lighter;
    color: rgb(255, 252, 242);
    letter-spacing: 1.5px;
  }

  h1 {
    margin: 50px auto;
  }

  .loader {
    position: relative;
    margin: 75px auto;
    width: 150px;
    height: 150px;
    display: block;
    overflow: hidden;
  }
  .loader div {
    height: 100%;
  }

  /* loader 1 */
  .loader1, .loader1 div {
    border-radius: 50%;
    padding: 8px;
    border: 2px solid transparent;
    -webkit-animation: rotate linear 3.5s infinite;
            animation: rotate linear 3.5s infinite;
    border-top-color: rgb(255, 252, 242);
    border-bottom-color: rgb(65, 184, 131);
  }
</style>
