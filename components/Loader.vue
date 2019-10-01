<template>
  <div style="margin-top: 60px">
    <div class='loader loader1'>
      <div>
        <div>
          <div>
            <div>
              <div>
                <div></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
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
      border-top-color: rgb(76, 126, 168);
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
      border-top-color: rgb(76, 126, 168);
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
    border-bottom-color: rgb(76, 126, 168);
  }

  /*loader 2  */
  .loader2, .loader2 div {
    border-radius: 50%;
    padding: 8px;
    border: 2px solid transparent;
    -webkit-animation: rotate linear 3.5s infinite;
            animation: rotate linear 3.5s infinite;
    border-top-color: rgb(76, 126, 168);
    border-left-color: rgb(255, 252, 242);
    border-right-color: rgb(255, 252, 242);
  }

  /*loader 3  */
  .loader3, .loader3 div {
    border-radius: 50%;
    padding: 8px;
    border: 2px solid transparent;
    -webkit-animation: rotate linear 3.5s infinite;
            animation: rotate linear 3.5s infinite;
    border-top-color: rgb(255, 252, 242);
    border-left-color: rgb(76, 126, 168);
    -webkit-animation-timing-function: cubic-bezier(0.55, 0.38, 0.21, 0.88);
            animation-timing-function: cubic-bezier(0.55, 0.38, 0.21, 0.88);
    -webkit-animation-duration: 3s;
            animation-duration: 3s;
  }

  /* loader 4 */
  .loader4, .loader4 div {
    border-radius: 50%;
    padding: 8px;
    border: 2px solid transparent;
    -webkit-animation: rotate linear 3.5s infinite;
            animation: rotate linear 3.5s infinite;
    border-radius: 50%;
    padding: 4px;
    -webkit-animation: rotate2 4s infinite linear;
            animation: rotate2 4s infinite linear;
  }

  div:hover {
    -webkit-animation-play-state: paused;
            animation-play-state: paused;
  }

  .loader, .loader * {
    will-change: transform;
  }
</style>
