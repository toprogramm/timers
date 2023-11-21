
<template>
<div id="clock">
  <v-card
      class="mx-auto my-8 px-2"
      width="fit-content"
      rounded="lg"
      theme="dark"
      title="SURVEY"
      align="center"
      justify="center"
    >
    <template v-slot:append>
      <div class="me-n2">
        <v-btn
          icon="$close"
          density="comfortable"
          variant="plain"
          @click="reset"
        ></v-btn>
      </div>
    </template>
    <v-card-title class="py-5 font-weight-black">{{ time }}</v-card-title>
    <v-container>
      <v-row justify="center" align="center">
        <v-col cols="auto">
          <v-btn id="toggle" min-width="112" size="x-large"  color="indigo-darken-3"  @click="toggleClock">{{ running ? 'Stop' : 'Start' }}</v-btn>
       </v-col>

       <v-col cols="auto">
          <v-btn id="send"  size="x-large" color="indigo-darken-3"  @click="sendData">Send</v-btn>
        </v-col>
     </v-row>
    </v-container>
  </v-card>  
  
  <!-- <div class="text">
    <a href="https://codepen.io/raphael_octau" target="_blank">@raphael_octau</a>
  </div> -->
</div>

  <v-bottom-navigation>
    <v-btn value="recent">
      <v-icon>mdi-history</v-icon>

      <span>Home</span>
    </v-btn>

    <v-btn value="favorites" @click="reset">
      <v-icon>mdi-heart</v-icon>

      <span>Favorites</span>
    </v-btn>

    <v-btn value="nearby">
      <v-icon>mdi-map-marker</v-icon>

      <span>Back</span>
    </v-btn>
  </v-bottom-navigation>
</template>
<script >

export default {
  data () { return {
    time: '00:00:00.000',
    timeBegan: null,
    timeStopped: null,
    stoppedDuration: 0,
    started: null,
    running: false
  }
},
  methods: {
    toggleClock: function() {
      if (this.running) {
        this.stop();
      } else {
        this.start();
      }
    },
    start: function() {
      if (this.running) return;

      if (this.timeBegan === null) {
        this.reset();
        this.timeBegan = new Date();
      }

      if (this.timeStopped !== null) {
        this.stoppedDuration += (new Date() - this.timeStopped);
      }

      this.started = setInterval(this.clockRunning, 10);
      this.running = true;
    },
    stop: function() {
      this.running = false;
      this.timeStopped = new Date();
      clearInterval(this.started);
    },
    reset: function() {
      this.running = false;
      clearInterval(this.started);
      this.stoppedDuration = 0;
      this.timeBegan = null;
      this.timeStopped = null;
      this.time = "00:00:00.000";
    },
    clockRunning: function() {
      var currentTime = new Date(),
        timeElapsed = new Date(currentTime - this.timeBegan - this.stoppedDuration),
        hour = timeElapsed.getUTCHours(),
        min = timeElapsed.getUTCMinutes(),
        sec = timeElapsed.getUTCSeconds(),
        ms = timeElapsed.getUTCMilliseconds();

      this.time =
        this.zeroPrefix(hour, 2) + ":" +
        this.zeroPrefix(min, 2) + ":" +
        this.zeroPrefix(sec, 2) + "." +
        this.zeroPrefix(ms, 3);
    },
    zeroPrefix: function(num, digit) {
      var zero = '';
      for (var i = 0; i < digit; i++) {
        zero += '0';
      }
      return (zero + num).slice(-digit);
    },
    sendData: function() {
      console.log(this.time); // Выводим текущее значение таймера в консоль
    }
  }
};

// export default {
//   name: 'TimerView',
  
// }
</script>

  
