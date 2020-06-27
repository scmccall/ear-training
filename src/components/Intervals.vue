<template>
  <div class="hello">
    <h1>Ear Training</h1>
    <button v-on:click='playButton'>Play</button>
    <p v-if="answerSelected">{{ correctOrNot }}</p>
    <div v-if="selectedInterval != ''" class=interval-list>
      <ul
        class="interval-button"
        v-for="interval in intervals"
        :key="interval.name"
        @click="[checkIfCorrect($event, interval), answerSelected=true]">
          {{ interval.name }}
      </ul>
    </div>
  </div>
</template>

<script>

const C4 = require("../assets/audio/C4.mp3");
const Db4 = require("../assets/audio/Db4.mp3");
const D4 = require("../assets/audio/D4.mp3");
const Eb4 = require("../assets/audio/Eb4.mp3");
const E4 = require("../assets/audio/E4.mp3");
const F4 = require("../assets/audio/F4.mp3");
const Gb4 = require("../assets/audio/Gb4.mp3");
const G4 = require("../assets/audio/G4.mp3");
const Ab4 = require("../assets/audio/Ab4.mp3");
const A4 = require("../assets/audio/A4.mp3");
const Bb4 = require("../assets/audio/Bb4.mp3");
const B4 = require("../assets/audio/B4.mp3");
const C5 = require("../assets/audio/C5.mp3");

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
          stepsFromC: 0,
          note: C4 },
        { name: "Minor Second",
          stepsFromC: 1,
          note: Db4 },
        { name: "Major Second",
          stepsFromC: 2,
          note: D4 },
        { name: "Minor Third",
          stepsFromC: 3,
          note: Eb4 },
        { name: "Major Third",
          stepsFromC: 4,
          note: E4 },
        { name: "Perfect Fourth",
          stepsFromC: 5,
          note: F4 },
        { name: "Tritone",
          stepsFromC: 6,
          note: Gb4 },
        { name: "Perfect Fifth",
          stepsFromC: 7,
          note: G4 },
        { name: "Minor Sixth",
          stepsFromC: 8,
          note: Ab4 },
        { name: "Major Sixth",
          stepsFromC: 9,
          note: A4 },
        { name: "Minor Seventh",
          stepsFromC: 10,
          note: Bb4 },
        { name: "Major Seventh",
          stepsFromC: 11,
          note: B4 },
        { name: "Octave",
          stepsFromC: 12,
          note: C5 },
      ],
      // the randomly selected interval
      selectedInterval: "",

      middleC: 'ear-training/src/assets/audio/songFileExample.mp3',

      // .correct and .incorrect CSS classes as variables
      correctClass: "correct",
      incorrectClass: "incorrect",

      // True if user has clicked an Interval, False otherwise
      answerSelected: false,

      // The text user will see once they selest an answer
      correctOrNot: "",

      // Number of miliseconds each note will play
      noteTimeout: 1500,
      
    }
  },

  methods: {

    playButton() {
      this.selectInterval();
      let firstNote = new Audio(this.getFirstNote());
      let secondNote = new Audio(this.getSecondNote());
      this.playNote(firstNote)
      setTimeout(() => {
        this.playNote(secondNote);
      }, this.noteTimeout);
    },

    getFirstNote() {
      return C4;
    },

    getSecondNote() {
      return this.selectedInterval.note;
    },

    playNote(note) {
      note.play();
      setTimeout(() => {
        note.pause();
      }, this.noteTimeout);
    },

    // Returns a random Interval from an array of Interval objects
    randomInterval: function(array) {
      let rand = Math.floor(Math.random()*array.length);
      return array[rand];
    },

    // returns an interval, selected by calling randomInterval
    selectInterval: function() {
      this.answerSelected = false;
      let interval = this.randomInterval(this.intervals);
      this.selectedInterval = interval;
      return interval.name
    },

    checkIfCorrect: function($event, interval) {
      if (interval === this.selectedInterval) {
        this.correctOrNot = "Correct! Click Play to try again";
      } else {
        this.correctOrNot = `Sorry, the correct answer is ${this.selectedInterval.name}. `
        + `Click Play to try again`;
      }
    }

  },

  computed: {

  }
}
</script>

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

/* CHANGE THE COLOURS HERE */
.correct{
  border: solid #1518ca;
  background-color: rgba(21, 39, 202, 0.1);
}

/* CHANGE THE COLOURS HERE */
.incorrect{
  border: solid #ca3f15;
  background-color: rgba(202, 57, 21, 0.1);
}

</style>
