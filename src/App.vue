<template>
<div class="wrapper">
  <div class="content-wrapper">
    <app-timer v-for="(item, i) in count" :key="i"></app-timer>
    <div class="add-button" @click="count++">+</div>
  </div>
</div>
</template>

<script>
import AppTimer from './components/Timer'

export default {


  data() {
    return {
      count: 1,
    }
  },

  components: {
    AppTimer,
  }
}
</script>

<style>

  * {
    box-sizing: border-box;
  }

  @font-face {
    font-family: "Gotham Pro";
    font-weight: normal;
    font-display: swap;
    src: url("/src/fonts/GothamPro.woff") format("woff");
  }

  body {
    min-width: 320px;
    margin: 0;

    font-family: "Gotham Pro", "Arial", sans-serif;

    background-color: #353638;
  }

  .wrapper {
    width: 775px;
    margin-top: 50px;
    margin-left: auto;
    margin-right: auto;
  }

  .content-wrapper {
    display: flex;
    flex-wrap: wrap;
    margin-left: -50px;
  }

  .add-button {
    position: relative;

    width: 225px;
    height: 120px;
    margin-left: 50px;
    padding: 40px;

    text-align: center;


    font-size: 50px;
    color: #9E9E9E;

    background-color: #696969;
  }

  .add-button:hover {
    color: #fff;
    opacity: 0.8;
    transition: all 0.3s
  }


  @media (max-width: 850px) {
      .wrapper {
        width: 500px;
      }
  }

  @media (max-width: 550px) {
    .wrapper {
      width: 320px;
    }

    .content-wrapper {
      margin: 0;
    }

    .timer {
      margin-left: 0;
    }
  } 

</style>