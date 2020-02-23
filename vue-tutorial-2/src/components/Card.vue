<template>
  <div class="card" v-bind:style="style">
    <div v-if="text === 'secret'">
      <img :src="image" class="image" />
    </div>
    <h2>{{ title }}</h2>

    <h4>{{ displayText }}</h4>

    <div>
      <!-- v-model = v-bind:value + v-on:input -->
      <h6>v-model</h6>
      <input v-model="text" />
    </div>

    <!-- <div>
      <h6>v-bind:value</h6>
      <input v-bind:value="text" />
    </div>

    <div>
      <h6>v-on:input</h6>
      <input v-on:input="text = $event.target.value">
    </div> -->
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: "Untitled"
    },
    defaultText: String,
    color: String,
    customMethod: Function
  },
  // computed is synchronous and does not allow side effect
  computed: {
    style() {
      if (this.text !== "flip") {
        return { backgroundColor: this.color, color: "#fff" }
      }

      return { color: this.color }
    },
    displayText() {
      if (!this.text || !this.customMethod) return

      return this.customMethod(this.text)
    }
  },
  // local state
  data() {
    return {
      text: this.defaultText,
      image: ''
    }
  },
  watch: {
    async text(value) {
      if(value === 'secret') {
        console.log(this.image)
        this.image = await this.getDogImage()
      }
    }
  },
  methods: {
    async getDogImage() {
      const response = await fetch('https://dog.ceo/api/breeds/image/random')
      const json = await response.json()
      return json.message
    }
  }
}
</script>

<style scoped>
.card {
  box-shadow: 0 0 0.5rem #aaa;
  padding: 1rem;
  margin: 1rem;
}

.image {
  width: 10rem;
}
</style>
