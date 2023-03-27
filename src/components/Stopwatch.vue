<script>
export default {
  emits: ['update:start', 'update:stop', 'update:reset'],
  props: ['stopwatch'],
  computed: {
    hours() {
      return Math.floor(this.stopwatch.time / 3600)
    },
    minutes() {
      return Math.floor((this.stopwatch.time / 60) % 60)
    },
    seconds() {
      return this.stopwatch.time % 60
    },
  },
  methods: {
    formatTime(timeValue) {
      return timeValue ? timeValue + ':' : ''
    },
  },
}
</script>
<template>
  <div class="stopwatch" :class="{ stopwatch_start: stopwatch.timerRunning }">
    <div class="stopwatch__timer">
      <span>{{ formatTime(hours) }}{{ formatTime(minutes) }}{{ seconds }}</span>
    </div>
    <div class="stopwatch__controls">
      <button
        class="stopwatch__start"
        @click="$emit('update:start', stopwatch.id)"
        v-show="!stopwatch.timerRunning"
      >
        <svg
          width="17"
          height="20"
          viewBox="0 0 17 20"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path d="M0 20V0L17 10L0 20Z" />
        </svg>
      </button>
      <button
        class="stopwatch__start"
        @click="$emit('update:stop', stopwatch.id)"
        v-show="stopwatch.timerRunning"
      >
        <svg
          width="10"
          height="20"
          viewBox="0 0 10 20"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <rect x="7" width="3" height="20" />
          <rect width="3" height="20" />
        </svg>
      </button>
      <button
        class="stopwatch__stop"
        @click="$emit('update:reset', stopwatch.id)"
      >
        <svg
          width="20"
          height="20"
          viewBox="0 0 20 20"
          xmlns="http://www.w3.org/2000/svg"
        >
          <rect width="20" height="20" />
        </svg>
      </button>
    </div>
  </div>
</template>
<style></style>
