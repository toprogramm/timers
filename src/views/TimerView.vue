<template>
<div id="clock">
  <div>{{ time }}</div>

  <div id="clock" v-for="(clock, index) in clocks" :key="index">
  <v-card
      class="mx-auto my-3 px-1"
      width="fit-content"
      rounded="lg"
      theme="dark"
      :title="clock.userData.cardName"
      align="center"
      justify="center"
      :color= "clock.userData.cardColor"
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
    <v-card-title class="py-5 font-weight-black text-h4">{{ clock.time }}</v-card-title>
    <v-container>
      <v-row justify="center" align="center">
        <v-col cols="auto">
          <v-btn id="toggle" min-width="112" size="x-large"  color="indigo-darken-3"  @click="toggleClock(index)">{{ running ? 'Stop' : 'Start' }}</v-btn>
       </v-col>

       <v-col cols="auto">
          <v-btn id="send"  size="small" color="indigo-darken-3"  @click="sendData">Send</v-btn>
        </v-col>
     </v-row>
    </v-container>
  </v-card></div>
  
 
  <!-- <div class="text">
    <a href="https://codepen.io/raphael_octau" target="_blank">@raphael_octau</a>
  </div> -->
</div>
<div 
    id="add" 
    align="center"
    justify="center"
    @click="addTimer">
  <v-btn
        class="ma-2"
        color="light-green-lighten-1"
        size="x-large"
      >
        ADD NEW
        <v-icon
          end
          icon="mdi-plus"
          size="x-large"
        ></v-icon>
  </v-btn> 
</div>

</template>
<script >

export default {
  data () { return { 
    time: '00:00:00.00',
    timeBegan: null,
    timeStopped: null,
    stoppedDuration: 0,
    started: null,
    running: false,
    userData: {
      cardName: "ENGLISH",
      cardColor:"#ff6600",
    }, 
    clocks: [],

  }
},
  methods: {
    addTimer: function() {
    this.clocks.push({
      time: '00:00:00.00',
      timeBegan: null,
      timeStopped: null,
      stoppedDuration: 0,
      started: null,
      running: false,
      userData: {
      cardName: "ENGLISH",
      cardColor:"#ff6600",
      },
    
    });
    console.log(this.clocks)
    this.reset();
    },
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
      this.time = "00:00:00.00";
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
        this.zeroPrefix(ms, 2);
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

  
