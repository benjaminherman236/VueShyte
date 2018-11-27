<template>
  <v-container>
    <word-window> </word-window>
    <h1>Typing Test </h1>
    <v-layout wrap v-if="!complete">
      <v-flex xs12>
        <v-text-field v-bind:style="{color: grade}" id="input" v-model="input" label="User Input"> </v-text-field>
      </v-flex>
      <v-btn @click="startTest" v-if="!started" v-model="started">Start</v-btn>
      <v-flex v-model="timeLimit">{{timeLimit}} </v-flex>
    </v-layout>
    <v-layout v-if="timeLimit == 0">
      <v-flex>
        <h1> Complete!</h1>
      </v-flex>
      <v-flex>
        <h2> Words Completed: </h2>
        <h2> Words Per Minute </h2>
      </v-flex>
      <v-btn @click="reset">Reset</v-btn>
    </v-layout>
  </v-container>
</template>

<script>
  import WordWindow from './Wordwindow.vue'
  export default {
    data() {
      return {
        input: "",
        grade: "black",
        correct: null,
        started: false,
        complete: false,
        timeLimit: 60,
        timer: ""
      }
    },
    methods: {
      reset() {
        this.timeLimit = 60
        this.started = false
      },
      startTest() {
        this.started = true
        this.startCounter()
      }
    },
    computed: {
      changeColor(correct) {
        if (correct) {
          this.grade = "green"
          return this.grade
        } else {
          this.grade = "red"
          return this.grade
        }
      },
      startCounter() {
        console.log('buh')
        this.timer = setInterval(() => {
          this.timeLimit -= 10;
          if (this.timeLimit == 0) {
            clearInterval(this.timer)
          }
          while (this.timeLimit >= 0) {
            return this.timeLimit
          }
        }, 1000)
      }
    },
    components: {
      wordWindow: WordWindow
    }
  }
</script>

<style>

</style>