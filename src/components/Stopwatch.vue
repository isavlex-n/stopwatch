<script>
export default {
  emits: ['update:toggle', 'update:reset'],
  props: ['stopwatch'],
  computed: {
    formatTime() {
      const seconds = Math.floor(this.stopwatch.elapsed / 1000)
      const minutes = Math.floor(seconds / 60)
      const hours = Math.floor(minutes / 60)
      const minutesStr = minutes ? (minutes % 60) + ':' : ''
      const hoursStr = hours ? hours + ':' : ''
      return `${hoursStr}${minutesStr}${seconds % 60}`
    }
  },
}
</script>
<template>
  <div class="stopwatch" :class="{ stopwatch_start: stopwatch.isRunning }">
    <div class="stopwatch__timer">
      <span>{{ formatTime }}</span>
    </div>
    <div class="stopwatch__controls">
      <button
        class="stopwatch__start"
        @click="$emit('update:toggle', stopwatch.id)"
        v-show="!stopwatch.isRunning"
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
        @click="$emit('update:toggle', stopwatch.id)"
        v-show="stopwatch.isRunning"
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
