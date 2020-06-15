<template>
  <div class="hello">
    <h1>Ear Training</h1>
    <ul v-for="interval in intervals" :key="interval">
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
      }
    }
  },
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
</style>
