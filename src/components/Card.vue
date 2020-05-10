<template>
  <li class="flip-container" :class="{
    flip: isRevealed
    }">
    <div class="flipper">
      <button
        class="front"
        v-on:click="reveal">
        {{id+1}}
        <span class="sr-only">Reveal</span>
      </button>
      <div
        class="back"
        v-bind:class="{
          group: type === 'group',
          solo: type === 'solo'
        }"
        v-on:click="hide">
        <div class="content">
          <span v-if="description">{{description}}</span>
          <div v-if="hasEgg" class="win-icon">💐</div>
        </div>
      </div>
    </div>
  </li>
</template>

<script>
export default {
  name: 'Card',
  props: {
    id: Number,
    hasEgg: Boolean,
    type: String,
    description: String,
    startRevealed: Boolean,
  },
  data: function() {
    return {
      isRevealed: this.startRevealed ? this.startRevealed : false,
    }
  },
  methods: {
    reveal: function() {
      this.isRevealed = true
      this.$emit('reveal-card')
    },
    hide: function() {
      this.isRevealed = false
      this.$emit('hide-card')
    }
  }
}
</script>

<style scoped>

.front,
.back {
  border-radius: 10px;
  box-shadow: 5px 5px 7px 0px rgba(0,0,0,0.4);
  color: rgba(0,0,0,0.8);
  overflow: scroll;
}

.front {
  background-image: url('https://scontent-lht6-1.xx.fbcdn.net/v/t1.15752-9/97315748_558912631705851_8137324624745594880_n.png?_nc_cat=108&_nc_sid=b96e70&_nc_ohc=Mi0MD4y243QAX-aqALc&_nc_ht=scontent-lht6-1.xx&oh=8f48f577ee31bfd267c7860d353dea35&oe=5EDCF486');
  color: #333;
  background-size: cover;
  background-position: center center;
  cursor: pointer;
  border: 0;
  font-size: 1.2em;
  font-weight: bold;
}

.back {
  background: white;
}

.back.group {
  background: #6dbff0;
}

.back.solo {
  background: #ef6eff;
}

.win-icon {
  font-size: 4em;
}

.sr-only {
  clip: rect(1px, 1px, 1px, 1px);
  clip-path: inset(50%);
  height: 1px;
  width: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
}

.content {
  padding: 0.5em;
}





/* entire container, keeps perspective */
.flip-container {
	perspective: 1000px;
}
	/* flip the pane when hovered */
	.flip-container.flip .flipper {
		transform: rotateY(180deg);
	}

.flip-container, .front, .back {
	width: 195px;
	height: 195px;
}

/* flip speed goes here */
.flipper {
	transition: 0.6s;
	transform-style: preserve-3d;

	position: relative;
}

/* hide back of pane during swap */
.front, .back {
	backface-visibility: hidden;

	position: absolute;
	top: 0;
	left: 0;
}

/* front pane, placed above back */
.front {
	z-index: 2;
	/* for firefox 31 */
	transform: rotateY(0deg);
}

/* back, initially hidden pane */
.back {
	transform: rotateY(180deg);
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
