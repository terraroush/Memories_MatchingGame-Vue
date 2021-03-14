<template>
  <div class="card" :class="{ flipped: isShown }">
    <div class="card-inner" @click="handleClick">
      <div class="backside">
        <img
          src="@/assets/images/black-flora-playing-cards.png"
          alt="hidden card"
        />
      </div>
      <div class="picSide">
        <img
          :src="require('@/assets/images/' + tripPics.image)"
          :alt="tripPics.name"
          :title="tripPics.name"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["tripPics", "guess1", "guess2"],

  methods: {
    handleClick() {
      this.$emit("select", this.language);
    },
  },
  computed: {
    isShown() {
      return this.tripPics.foundMatch ||
        this.tripPics === this.guess1 ||
        this.tripPics === this.guess2
    },
  },
};
</script>

<style scoped>
img {
  height: 200px;
}
.card {
  background-color: transparent;
  width: 100px;
  height: 100px;
  perspective: 1000px;
  margin-top: 20px;
}
.card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}
.flipped .card-inner {
  transform: rotateY(180deg);
}
.backside,
.picSide {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}
.backside {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: auto 60px;
}
.picSide {
  color: black;
  transform: rotateY(180deg);
}
</style>
