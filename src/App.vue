<template>
  <div id="app">
    <div class="left">
      <h1>Holiday Hunt</h1>
      <h2>You could find...</h2>
      <ul class="legend">
        <Card :id="1" :hasEgg="true" :startRevealed="true" />
        <Card :id="2" type="solo" description="A solo challenge" :startRevealed="true" />
        <Card :id="3" type="group" description="A group challenge" :startRevealed="true" />
      </ul>
    </div>
    <ul class="list">
      <Card
        v-for="item in items"
        :key="item.id"
        v-bind="item"
        v-on:reveal-card="nextTurn"
        v-on:hide-card="undoTurn" />
    </ul>
    <Players :players="players" :activePlayer="activePlayer" />
  </div>
</template>

<script>
import Card from './components/Card.vue'
import Players from './components/Players.vue'
import { items, players } from './data.json';

export default {
  name: 'App',
  components: {
    Card,
    Players
  },
  data: () => ({
    items: items.map((item, index) => ({
      id: index,
      ...item,
    })),
    players,
    activePlayer: 0
  }),
  methods: {
    nextTurn: function() {
      this.activePlayer = (this.activePlayer + 1) % players.length;
    },
    undoTurn: function() {
      this.activePlayer = (this.activePlayer - 1) % players.length;
    },
  }
}
</script>

<style>
html  {
  background: linear-gradient(45deg, #3932FF 10%, #C832FF 90%);
  background-size: 100%;
  color: white;
}

body {
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  margin: 0 20px;
  display: flex;
  height: 100vh;
}

.left {
  margin-top: 60px;
  flex-basis: 20%;
}

h1 {
  width: 4em;
  font-size: 4.5em;
  margin: 0 0 1em;
  line-height: 1.1em;
}

.list {
  flex-basis: 60%;
  align-self: center;
  display: grid;
  grid-template-columns: repeat(5,1fr);
  margin: 0;
  padding: 0;
  list-style-type: none;
  place-items: start;
  grid-gap: 0.5em;
}

.players {
  flex-basis: 20%;
  margin-top: 60px;
}

.legend {
  list-style-type: none;
  width: 150px;
  padding: 0;
  margin: 0;
}

.legend li + li {
  margin-top: 1em;
}
</style>
