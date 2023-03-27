<script>
export default {
  emits: ['update:add']
}
</script>
<template>
  <div class="stopwatch stopwatch_add">
    <button @click="$emit('update:add')">
      <svg
        width="20"
        height="20"
        viewBox="0 0 20 20"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <rect x="8.5" width="3" height="20" />
        <rect y="11.5" width="3" height="20" transform="rotate(-90 0 11.5)" />
      </svg>
    </button>
  </div>
</template>
