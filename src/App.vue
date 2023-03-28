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
        isRunning: false,
        elapsed: 0,
        lastTick: null,
      })
    },
    toggleTimer(id) {
      const stopwatch = this.stopwatches.find(
        (stopwatch) => stopwatch.id === id,
      )
      stopwatch.isRunning = !stopwatch.isRunning
      if (stopwatch.isRunning) {
        stopwatch.lastTick = Date.now()
        this.tick(stopwatch)
      }
    },
    tick(stopwatch) {
      const now = Date.now()
      const delta = now - stopwatch.lastTick
      stopwatch.lastTick = now
      if(stopwatch.isRunning) {
        stopwatch.elapsed += delta
        requestAnimationFrame(() => {
          this.tick(stopwatch)
        })
      }
    },
    resetTimer(id) {
      const stopwatch = this.stopwatches.find(
        (stopwatch) => stopwatch.id === id,
      )
      stopwatch.isRunning = false
      stopwatch.elapsed = 0
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
        @update:toggle="toggleTimer($event)"
        @update:reset="resetTimer($event)"
      ></stopwatch>
      <stopwatch-add @update:add="addStopwatch"></stopwatch-add>
    </main>
  </div>
</template>

<style scoped></style>
