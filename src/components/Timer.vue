<template>
  <div class="timer">
    <div class="timer__face" :class="timerActive">
        <span class="timer__num--hours" :class="timerActive" v-show="hours !== '0'">{{ hours + ':' }}</span>
        <span class="timer__num" :class="timerActive" v-show="minutes !== '0' || hours !== '0'">{{ minutes + ':' }}</span>
        <span class="timer__num timer__num--sec" :class="timerActive" >{{ seconds }}</span>

    </div>
    <div class="timer__controls">
      <span class="timer__button" :class="timerActive" v-if="!active" @click="start">
        <img src="src/img/play.svg" alt="">
      </span>
      <span class="timer__button" :class="timerActive" v-else @click="pause">
        <img src="src/img/pause.svg" alt="">
      </span>
      <span class="timer__button" :class="timerActive" @click="reset">
        <img src="src/img/stop.svg" alt="">
      </span>
    </div>
  </div>
</template>

<script>
export default {

  data() {
    return {
      hours: '1',
      minutes: '59',
      seconds: '58',

      interval: 0,
      active: false,
    }
  },

  methods: {
    tick() {
      this.seconds++;

      if(this.seconds > '59') {
        this.seconds = '0';
        this.minutes++
      }

      if(this.minutes >'59') {
        this.minutes = '0'
        this.hours++
      }
    },

    start() {
      this.active = true;
      this.interval = setInterval(this.tick, 1000);
    },

    pause() {
      this.active = false;
      clearInterval(this.interval);
    },

    reset() {
      clearInterval(this.interval);
      this.active = false;
      this.seconds = '0';
      this.minutes = '0';
      this.hours = '0';
    },
  },

  computed: {
    timerActive() {
      return this.active ? 'timer--active' : '';
    }
  },
}
</script>

<style>
  .timer {
    width: 225px;
    height: 120px;
    margin-bottom: 50px;
    margin-left: 50px;

    background-color: #696969;
  }

  .timer__face,
  .timer__controls {
    height: 50%;
    display: flex;
    justify-content: center;
    padding: 20px 30px;

    font-family: "Gotham Pro", "Arial", sans-serif;
    font-size: 22px;
  }

  .timer__face {
    position: relative;
  }

  .timer__num {
    min-width: 16px;
    text-align: center;
  }

  .timer__num--hours {
    width: 32px;
    text-align: right;
  }

  .timer__num--sec {
    width: 32px;
    text-align: left;
  }

  .timer__controls {
    justify-content: space-around;

    padding-left: 60px;
    padding-right: 60px;
  }

  .timer__button {
    opacity: 0.4;
  }

  .timer__button:hover {
    transform: scale(1.2);
    transition: all 0.3s
  }

  .timer__controls span {
    width: 20px;
    height: 20px;
  }

  .timer__face::after {
    content: '';

    position: absolute;
    bottom: 0;

    width: 100%;
    height: 2px;

    background-color: #fff;
    opacity: 0.4;
  }

  .timer__face span {
    color: #fff;
    opacity: 0.4;
  }


   .timer--active,
   .timer--active::after {
     opacity: 1 !important;
   }


</style>