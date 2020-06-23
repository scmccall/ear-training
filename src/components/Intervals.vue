<template>
  <div class="hello">
    <h1>Ear Training</h1>
    <button v-on:click='playNote'>Play</button>
  </div>
</template>

<script>

const someSound = require("../assets/audio/middleC.mp3");

export default {
  name: 'Intervals',
  data: function() {
    return {
      someSound,
    }
  },

  methods: {
    // Selects a note 
    getNote: function() {
      return this.someSound;
    },

    // Plays a note, selected via getNote()
    playNote: function() {
      let note = new Audio(this.getNote);
      console.log(`note = ${note.src}`);
      
      note.addEventListener("canplay", () => {
        console.log(`sound has been loaded`);
        note.play();
      });
    },
  },
}
</script>