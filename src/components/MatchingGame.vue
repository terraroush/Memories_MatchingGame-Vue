<template>
  
</template>

<script>
import getTripPicsCards from "../data";
import shuffle from "lodash.shuffle";

export default {
data() {
    return {
        tripPics: shuffle(getTripPicsCards()),
        guess1: null,
        guess2: null,
    }
}
}
</script>

<style>

</style>