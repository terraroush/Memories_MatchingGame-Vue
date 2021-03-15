<template>
  <div>
      <h1 class="neon">Thailand Memories Memory Game</h1>
    <h2 v-if="foundAllMatches">Congrats! You found them!</h2>
    <h2 v-else>Find all the matches</h2>
    <div class="game-board">
      <div v-for="tripPic in tripPics" :key="tripPic.id" class="cell">
        <card
          :tripPics="tripPic"
          @select="handleCardClick"
          :guess1="guess1"
          :guess2="guess2"
        />
      </div>
    </div>
  </div>
</template>

<script>
import getTripPicsCards from "../data";
import shuffle from "lodash.shuffle";
import Card from "./Card.vue";

export default {
  components: { Card },
  data() {
    return {
      tripPics: shuffle(getTripPicsCards()),
      guess1: null,
      guess2: null,
    };
  },
  methods: {
    handleCardClick(tripPicClicked) {
      // if there are two cards already flipped prevent a third from being flipped
      if (this.guess1 && this.guess2) return;
      // if the user clicked the same card twice don't do anything
      if (this.guess1 === tripPicClicked) return;
      if (this.guess1 === null) {
        this.guess1 = tripPicClicked;
        return;
      }
      this.guess2 = tripPicClicked;
      const [pic1, pic2] = this.getMatchingPics(tripPicClicked.name);
      if (this.guess1.name === this.guess2.name) {
        pic1.foundMatch = true;
        pic2.foundMatch = true;
        this.guess1 = null;
        this.guess2 = null;
      } else {
        setTimeout(() => {
          // user made two wrong guesses. Wait 2 seconds and flip cards
          this.guess1 = null;
          this.guess2 = null;
        }, 1500);
      }
    },
    getMatchingPics(name) {
      return this.tripPics.filter((p) => p.name === name);
    },
  },
  computed: {
    foundAllMatches() {
      return this.tripPics.every((p) => p.foundMatch);
    },
  },
};
</script>

<style scoped>

.neon {
    margin-bottom: 0;
  color: #fff;
  text-shadow:
    0 0 5px #fff,
    0 0 10px #fff,
    0 0 20px #fff,
    0 0 40px #0ff,
    0 0 80px #0ff,
    0 0 90px #0ff,
    0 0 100px #0ff,
    0 0 150px #0ff,
    0 0 180px #0ff,
    0 0 200px #0ff;
}
.game-board {
  display: flex;
  flex-wrap: wrap;
  align-items: space-between;
  justify-content: center;
}
/* .cell {
  padding: 10px;
} */
</style>
