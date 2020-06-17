<template>
  <div class="hello">
    <h1>Ear Training</h1>
    <button v-on:click='playNote'>Play</button>
    <button v-on:click='selectInterval'>Pick Interval</button>
    <p> The selected interval is {{ selectedInterval.name }}</p>
    <ul
      class="interval-button"
      v-for="interval in intervals"
      :key="interval.name">
      {{ interval.name }}
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
      // Array of Interval objects that describe musical intervals spanning
      // from Unison to Octave
        // name: (String) name of the interval
        // stepsFromC: (Int) number of steps from Middle C (aka C4)
      intervals: [
        { name: "Unison",
          stepsFromC: 0 },
        { name: "Minor Second",
          stepsFromC: 1 },
        { name: "Major Second",
          stepsFromC: 2 },
        { name: "Minor Third",
          stepsFromC: 3 },
        { name: "Major Third",
          stepsFromC: 4 },
        { name: "Perfect Fourth",
          stepsFromC: 5 },
        { name: "Tritone",
          stepsFromC: 6 },
        { name: "Perfect Fifth",
          stepsFromC: 7 },
        { name: "Minor Sixth",
          stepsFromC: 8 },
        { name: "Major Sixth",
          stepsFromC: 9 },
        { name: "Minor Seventh",
          stepsFromC: 10 },
        { name: "Major Seventh",
          stepsFromC: 11 },
        { name: "Octave",
          stepsFromC: 12}
      ],
      selectedInterval: "",

      middleC: 'ear-training/src/assets/audio/songFileExample.mp3'
      
    }
  },

  methods: {
    // Selects a note 
    getNote: function() {
      return this.middleC;
    },

    // Plays a note, selected via getNote()
    playNote: function() {
      console.log(`this.getNote = ${this.getNote}`);
      let note = new Audio(this.getNote);
      console.log(note);
      note.play();
      console.log(`playedparts = ${note.played}`);
      // alert("note played successfully");
    },

    // Returns a random Interval from an array of Interval objects
    randomInterval: function(array) {
      let rand = Math.floor(Math.random()*array.length);
      return array[rand];
    },

    // returns an interval, selected by calling randomInterval
    selectInterval: function() {
      let interval = this.randomInterval(this.intervals);
      this.selectedInterval = interval;
      return interval.name
    }
  },

  computed: {
    
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

.interval-button:hover {
  border: solid #15cac1;
  background-color: rgb(21, 202, 193, .1);
}

.interval-button:active {
  border: solid rgb(19, 199, 58);
  background-color: rgb(19, 199, 58, .1);
}

.interval-button:hover {
  border: solid #15cac1;
  background-color: rgb(21, 202, 193, .1);
}

/* CHANGE THIS */
.interval-button:hover .correct{
  border: solid #1518ca;
  background-color: rgba(21, 39, 202, 0.1);
}

/* CHANGE THIS */
.interval-button:hover .incorrect{
  border: solid #ca3f15;
  background-color: rgba(202, 57, 21, 0.1);
}

</style>
