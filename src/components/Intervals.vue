<template>
  <div class="hello">
    <h1>Ear Training</h1>
    <button v-on:click='playNote'>Play</button>
  </div>
</template>

<script>
const someSound = require("../assets/audio/middleC.mp3");

console.log(`somesound = ${someSound}`);

export default {
  name: "Intervals",
  data: () => ({
    someSound
  }),
  methods: {
    playNote() {
      console.log('calling playNote()');
      let note = new Audio(this.someSound);

      note.addEventListener("canplaythrough", () => { 
        console.log('event listener called');
        note.play();
      });
    }
  }
};
</script>