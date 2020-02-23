<template>
  <div class="card" ref="card">
    <h1>Card {{ id }}</h1>
    <h4>{{ text }}</h4>
    <input v-model="text" />
  </div>
</template>

<script>
export default {
  props: {
    id: Number,
    isDelayed: {
      type: Boolean,
      default: false,
    }
  },
  computed: {
    doubleText() {
      return this.text + " " + this.text
    }
  },
  data() {
    return {
      text: "Card Text"
    }
  },
  beforeCreate() {
    // Error, not able to use these inside beforeCreate
    // this.$emit("updateLog", `beforeCreated: Card ${this.id}`)
    // this.updateLog('beforeCreate')
    this.$emit(
      "updateLog",
      `beforeCreated: computed: doubleText: <span class="important">${this.doubleText}</span>`
    )
    this.$emit(
      "updateLog",
      `beforeCreated: data: text: <span class="important">${this.text}</span>`
    )
  },
  async created() {
    if (this.isDelayed) {
      await new Promise(resolve => {
        setTimeout(() => {
          resolve()
        }, 3000)
      })
    }

    this.updateLog('created')
  },
  beforeMount() {
    this.updateLog('beforeMount')
  },
  async mounted() {
    this.updateLog('mounted')
  },
  beforeUpdate() {
    this.updateLog('beforeUpdate')
  },
  updated() {
    this.updateLog('updated')
  },
  beforeDestroy() {
    this.updateLog('beforeDestroyed')
  },
  destroyed() {
    this.updateLog('destroyed')
  },
  methods: {
    updateLog(lifecycle) {
      this.$emit("updateLog", `${lifecycle}: Card ${this.id}`)
      this.$emit("updateLog", `${lifecycle}: computed: doubleText: ${this.doubleText}`)
      this.$emit("updateLog", `${lifecycle}: data: text: ${this.text}`)
      console.log(this.$refs.card)
    }
  }
}
</script>

<style scoped>
.card {
  width: 50rem;
  box-shadow: 0 0 0.5rem #555;
  padding: 1rem;
  margin: 1rem;
}
</style>
