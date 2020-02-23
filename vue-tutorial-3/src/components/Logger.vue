<template>
  <div class="logger">
    <template v-if="logs.length === 0">
      <div class="center">
        <h2>No Logs</h2>
      </div>
    </template>
    <template v-else>
      <ol>
        <li v-for="(log, index) in logs" :key="index" v-html="log"></li>
      </ol>
    </template>
  </div>
</template>

<script>
export default {
  props: {
    logs: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style scoped>
.logger {
  background-color: #222;
  color: #f8f8f8;
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  height: 50vh;
  padding: 0 1rem;
  overflow: scroll;
}

.center {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

ol {
  text-align: left;
}
</style>
