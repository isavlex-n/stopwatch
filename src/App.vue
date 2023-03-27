<script>
import Stopwatch from './components/Stopwatch.vue'
import StopwatchAdd from './components/StopwatchAdd.vue'
export default {
  data() {
    return {
      stopwatches: [],
    }
  },
  methods: {
    addStopwatch() {
      this.stopwatches.push({
        id: Date.now(),
        time: 0,
        timerRunning: false,
        timer: null,
      })
    },
    startTimer(id) {
      const stopwatch = this.stopwatches.find(
        (stopwatch) => stopwatch.id === id,
      )
      stopwatch.timerRunning = true
      stopwatch.timer = setInterval(() => {
        stopwatch.time++
      }, 1000)
    },
    stopTimer(id) {
      const stopwatch = this.stopwatches.find(
        (stopwatch) => stopwatch.id === id,
      )
      stopwatch.timerRunning = false
      clearInterval(stopwatch.timer)
    },
    resetTimer(id) {
      const stopwatch = this.stopwatches.find(
        (stopwatch) => stopwatch.id === id,
      )
      stopwatch.timerRunning = false
      stopwatch.time = 0
      clearInterval(stopwatch.timer)
    },
  },
  components: {
    Stopwatch,
    StopwatchAdd,
  },
}
</script>

<template>
  <div class="wrapper">
    <main>
      <stopwatch
        v-for="stopwatch in stopwatches"
        :stopwatch="stopwatch"
        @update:start="startTimer($event)"
        @update:stop="stopTimer($event)"
        @update:reset="resetTimer($event)"
      ></stopwatch>
      <stopwatch-add @update:add="addStopwatch"></stopwatch-add>
    </main>
  </div>
</template>

<style scoped></style>
