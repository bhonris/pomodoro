<template>
  <div>
    <h2 id="time">{{showMinutes}}:{{showSeconds}}</h2>
    <h3>{{state}}</h3>
    <br />Work Time:
    <input type="text" v-model="work" />
    <br />Rest Time:
    <input type="text" v-model="rest" />
    <br />
    <button v-on:click="switchTimer">{{getButtonName}}</button>
  </div>
</template>
<script>
export default {
  name: "Timer",
  data: function() {
    return {
      work: 15,
      rest: 5,
      currentTime: 0,
      CONST: 60,
      timer: null,
      buttonStart: true,
      state: "stop"
    };
  },
  methods: {
    switchTimer: function() {
      if (this.state === "stop") {
        this.currentTime = this.work * this.CONST;
        this.timer = setInterval(() => this.countdown(), 1000);
        this.state = "start";
        var audio = new Audio(require("../assets/start.wav"));
        audio.play();
      } else {
        clearInterval(this.timer);
        this.timer = null;
        this.state = "stop";
      }
    },
    countdown: function() {
      this.currentTime--;
    }
  },
  computed: {
    showMinutes: function() {
      const minutes = Math.floor(this.currentTime / this.CONST);
      return minutes.toString().padStart(2, "0");
    },
    showSeconds: function() {
      const seconds = this.currentTime % this.CONST;
      return seconds.toString().padStart(2, "0");
    },
    getButtonName: function() {
      if (this.state === "stop") return "Start";
      return "Stop";
    }
  },
  watch: {
    currentTime: function(newVal) {
      if (newVal > 0) return;
      if (this.state === "start") {
        this.state = "rest";
        this.currentTime = this.rest * this.CONST;
        var audio = new Audio(require("../assets/rest.wav"));
        audio.play();
        return;
      }
      if (this.state === "rest") {
        this.state = "start";
        this.currentTime = this.work * this.CONST;
        audio = new Audio(require("../assets/start.wav"));
        audio.play();

        return;
      }
    }
  }
};
</script>