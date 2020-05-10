<template>
  <li>
    <div class="name">
      {{name}}
      <button v-on:click="increment">+</button>
      <button v-on:click="decrement" :disabled="score === 0" class="decrement">-</button>
    </div>
    <div class="score">
      <span v-for="(point, index) in score" :key="index">💐</span>
    </div>
  </li>
</template>

<script>
export default {
  name: 'Player',
  props: {
    name: String,
  },
  data: () => ({
    score: 0
  }),
  methods: {
    increment: function() {
      this.score += 1;
    },
    decrement: function() {
      this.score -= 1;
    }
  }
}
</script>

<style scoped>
.name {
  font-size: 1.2em;
}
button {
  font-size: 0.7em;
}
button:not(:disabled) {
  cursor: pointer;
}
.score {
  font-size: 2em;
}
.decrement {
  background: transparent;
  border: 0;
}
</style>