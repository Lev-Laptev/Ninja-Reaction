<template>
  <h1>Ninja Reaction Timer</h1>
  <button
    @click="start"
    :disabled="isPlaying"
  >
    Play
  </button>
  <app-block
    v-if="isPlaying"
    :delay="delay"
    @endGame="endGame"
  />
  <app-results
    v-if="showResults"
    :score="score"
  />
</template>

<script>
import AppBlock from '@/components/AppBlock'
import AppResults from '@/components/AppResults'

export default {
  name: 'AppReaction',
  components: {
    AppBlock,
    AppResults
  },
  data: () => ({
    isPlaying: false,
    delay: null,
    score: null,
    showResults: false
  }),
  methods: {
    start () {
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true
      this.showResults = false
    },
    endGame (reactionTime) {
      this.score = reactionTime
      this.isPlaying = false
      this.showResults = true
    }
  }
}
</script>

<style>
#app {
  margin-top: 60px;

  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #444444;
  text-align: center;
}

button {
  margin: 10px;
  padding: 8px 16px;

  color: #ffffff;
  font-size: 16px;
  letter-spacing: 1px;

  background-color: #0faf87;
  border-radius: 4px;
  border: none;
  cursor: pointer;
}

button:disabled {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
