<template>
  <div class="players">
      <h2>Players</h2>
      <p>First to 5 wins!</p>
      <ul>
        <Player 
          v-for="(player, index) in players"
          :key="index"
          :name="player"
          :class="{
            'active-player': activePlayer === index
          }" />
      </ul>
    </div>
</template>

<script>
import Player from './Player';

export default {
  name: 'Players',
  props: {
    players: Array,
    activePlayer: Number,
  },
  components: {
    Player
  },
}
</script>

<style scoped>
.players {
  margin-left: 2em;
  width: 15em;
  font-size: 1.2em;
}

h2 {
  margin: 0 0 0.5em;
  font-size: 2em;
}

ul {
  margin: 0;
  padding-left: 1.2em;
  list-style-type: none;
}

.active-player {
  list-style-type: '⭐️';
}
</style>