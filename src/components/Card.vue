<template>
  <div class="card" :class="{ flipped: isShown }">
    <div class="card-inner" @click="handleClick">
      <div class="backside">
        <img
          class="back"
          src="@/assets/images/black-flora-playing-cards.jpeg"
          alt="hidden card"
        />
      </div>
      <div class="picSide">
        <img
          class="pic"
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
      this.$emit("select", this.tripPics);
    },
  },
  computed: {
    isShown() {
      return (
        this.tripPics.foundMatch ||
        this.tripPics === this.guess1 ||
        this.tripPics === this.guess2
      );
    },
  },
};
</script>

<style scoped>
img,
.pic {
  height: 150px;
  border-radius: 10px;
}

.card {
  background-color: transparent;
  width: 120px;
  height: 150px;
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
  margin-top: 3px;
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

.picSide {
  color: black;
  transform: rotateY(180deg);
}
</style>
