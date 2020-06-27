<template>
  <div class="hello">
    <h1>Ear Training</h1>
    <button v-on:click='playButton'>Play</button>
    <button v-on:click='selectInterval'>Pick Interval</button>
    <p> The selected interval is {{ selectedInterval.name }}</p>
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
const Fs4 = require("../assets/audio/Fs4.mp3");

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
              console.log('yelp!');
      }, this.noteTimeout);
    },

    getFirstNote() {
      return C4;
    },

    getSecondNote() {
      return Fs4;
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
      console.log(`interval = ${interval.name}`);
      if (interval === this.selectedInterval) {
        console.log(`true: ${interval} === ${this.selectedInterval}`);
        this.correctOrNot = "Correct! Click Play to try again";
      } else {
        console.log(`false: ${interval} =/= ${this.selectedInterval}`);
        this.correctOrNot = `Sorry, the correct answer is ${this.selectedInterval.name}`
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
