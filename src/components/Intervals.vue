<template>
  <div class="hello">
    <h1>Ear Training</h1>
    <button v-on:click='playNote()'>Play</button>
    <ul class="interval-button" v-for="interval in intervals" :key="interval">
      {{ interval }}
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Intervals',
  props: {

  },

  data: function() {
    return {
      intervals: {
        uni: "Unison",
        min2: "Minor Second",
        maj2: "Major Second",
        min3: "Minor Third",
        maj3: "Major Third",
        fourth: "Perfect Fourth",
        tri: "Tritone",
        fifth: "Perfect Fifth",
        min6: "Minor Sixth",
        maj6: "Major Sixth",
        min7: "Minor Seventh",
        maj7: "Major Seventh",
        oct: "Octave"
      },
      middleC: "ear-training/src/assets/audio/Piano.pp.C5.aiff"
    }
  },

  methods: {
    playNote: function() {
      let note = new Audio(this.getNote);
      alert(note);
      note.play();
      alert("note played successfully");
    }
  },

  computed: {
    getNote: function() {
      return this.middleC;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.interval-button {
  width: 20rem;
  border: solid lightseagreen;
}

</style>
