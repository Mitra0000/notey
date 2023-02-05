<template>
  <div class="row mt-4" style="text-align: center;">
      <h1 class="display-1" ref="timer">{{ strtime }}</h1>
  </div>
  <div class="row">
    <div class="col-lg d-flex" style="align-items: baseline;">
      <div class="no-grow">
        <button class="btn btn-light rounded" @click="$emit('download-notes')">
          <i class="bi bi-download"></i>
        </button>
      </div>
      <div class="btn-group-lg d-flex" style="flex-grow: 1; justify-content: center;">
        <button class="btn btn-primary" @click="startTimer()">Start</button>
        <button class="btn" @click="pauseTimer()">Pause</button>
        <button class="btn" @click="resetTimer()">Reset</button>
      </div>
      <div class="no-grow">
        <button class="btn btn-light rounded" @click="$emit('copy-to-clipboard')">
          <i class="bi bi-files"></i>
        </button>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "TimerComponent",
  data() {
    return {
      time: 0,
      strtime: "00:00",
      incrementTimer: {},
      isRunning: false,
    }
  },
  methods: {
    startTimer() {
      if (this.isRunning) return;
      this.isRunning = true;
      this.incrementTimer = setInterval(() => {
        this.time = this.time + 1;
        this.strtime = String(Math.floor(this.time / 60)).padStart(2, "0") + ":" + String(this.time % 60).padStart(2, "0");
      }, 1000);
    },
    pauseTimer() {
      this.isRunning = false;
      clearInterval(this.incrementTimer);
    },
    resetTimer() {
      this.time = 0;
      this.strtime = "00:00";
    },
    getTime() {
      return this.strtime;
    },
  }
}

</script>

<style>
</style>