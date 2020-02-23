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
    // cannot read id of undefined
    // this.$emit("updateLog", `beforeCreated: Card ${this.id}`)

    this.$emit(
      "updateLog",
      `beforeCreated: computed: doubleText: <span class="important">${this.doubleText}</span>`
    )
    this.$emit(
      "updateLog",
      `beforeCreated: data: text: <span class="important">${this.text}</span>`
    )

    this.$emit(
      "updateLog",
      `beforeCreated: refs: card: <span class="important">${this.$refs.card}</span>`
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

    this.$emit("updateLog", `created: Card ${this.id}`)
    this.$emit("updateLog", `created: computed: doubleText: ${this.doubleText}`)
    this.$emit("updateLog", `created: data: text: ${this.text}`)
    this.$emit(
      "updateLog",
      `created: refs: card: <span class="important">${this.$refs.card}</span>`
    )
  },
  beforeMount() {
    this.$emit("updateLog", `beforeMount: Card ${this.id}`)
    this.$emit(
      "updateLog",
      `beforeMount: computed: doubleText: ${this.doubleText}`
    )
    this.$emit("updateLog", `beforeMount: data: text: ${this.text}`)
    this.$emit(
      "updateLog",
      `beforeMount: refs: card: <span class="important">${this.$refs.card}</span>`
    )
  },
  async mounted() {
    this.$emit("updateLog", `mounted: Card ${this.id}`)
    this.$emit("updateLog", `mounted: computed: doubleText: ${this.doubleText}`)
    this.$emit("updateLog", `mounted: data: text: ${this.text}`)
    console.log(this.$refs.card)
  },
  beforeUpdate() {
    this.$emit("updateLog", `beforeUpdate: Card ${this.id}`)
    this.$emit(
      "updateLog",
      `beforeUpdate: computed: doubleText: ${this.doubleText}`
    )
    this.$emit("updateLog", `beforeUpdate: data: text: ${this.text}`)
    console.log(this.$refs.card)
  },
  updated() {
    this.$emit("updateLog", `updated: Card ${this.id}`)
    this.$emit("updateLog", `updated: computed: doubleText: ${this.doubleText}`)
    this.$emit("updateLog", `updated: data: text: ${this.text}`)
    console.log(this.$refs.card)
  },
  beforeDestroy() {
    this.$emit("updateLog", `beforeDestroy: Card ${this.id}`)
    this.$emit(
      "updateLog",
      `beforeDestroy: computed: doubleText: ${this.doubleText}`
    )
    this.$emit("updateLog", `beforeDestroy: data: text: ${this.text}`)
    console.log(this.$refs.card)
  },
  destroyed() {
    this.$emit("updateLog", `destroy: Card ${this.id}`)
    this.$emit("updateLog", `destroy: computed: doubleText: ${this.doubleText}`)
    this.$emit("updateLog", `destroy: data: text: ${this.text}`)
    console.log(this.$refs.card)
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
