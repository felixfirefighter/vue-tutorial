<template>
  <div id="app">
    <template v-for="card in cards">
      <!-- <Card
        v-bind:key="card.id"
        v-bind:title="card.title"
        v-bind:defaultText="card.defaultText"
        v-bind:color="card.color"
        v-bind:customMethod="card.customMethod"
      /> -->
      <Card :key="card.id" v-bind="card" />
    </template>
  </div>
</template>

<script>
import Card from "./components/Card"

export default {
  name: "App",
  components: {
    Card
  },
  data() {
    return {
      cards: [
        {
          id: 1,
          title: "Reverse String",
          defaultText: "Reverse input string",
          color: '#f8b500',
          customMethod: (value) => {
            return value.split('').reverse().join('')
          }
        },
        {
          id: 2,
          title: "Sort alphabetically",
          color: "#cb2d3e",
          customMethod: (value) => {
            return value.split('').sort().join('')
          }
        },
        {
          id: 3,
          defaultText: "This card has no title",
          color: '#085078'
        }
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  justify-content: center;
  padding: 0 2rem;
}

h6 {
  margin: .1rem;
}

</style>
