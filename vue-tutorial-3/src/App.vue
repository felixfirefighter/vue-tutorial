<template>
  <div id="app">
    <button @click="add">Add Card</button>
    <button @click="remove">Remove Card</button>
    <button @click="clear">Clear Logs</button>
    <div><input type="checkbox" v-model="isDelayed"/> <label>Delay created</label></div>

    <div class="card-list">
      <Card
        v-for="card in cards"
        v-bind="card"
        :key="card.id"
        :isDelayed="isDelayed"
        @updateLog="updateLog"
      />
    </div>
    <Logger :logs="logs" />
  </div>
</template>

<script>
import Card from "./components/Card"
import Logger from "./components/Logger"

export default {
  name: "App",
  components: {
    Card,
    Logger
  },
  data() {
    return {
      cards: [],
      logs: [],
      isDelayed: false,
    }
  },
  methods: {
    add() {
      this.cards.push({
        id: this.cards.length + 1
      })
    },
    remove() {
      this.cards.splice(-1, 1)
    },
    updateLog(log) {
      console.log(log)
      this.logs.push(log)
    },
    clear() {
      this.logs = []
    }
  }
}
</script>

<style>
html,
body {
  padding: 0;
  margin: 0;
  height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-bottom: 50vh;
}

.card-list {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.important {
  color: red;
}
</style>
