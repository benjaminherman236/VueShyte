<template>
<v-layout>
  <v-flex v-model="wordList"> {{wordList}}
  </v-flex>
</v-layout>
</template>

<script>
  const dictionary = [];
  const english = 'https://raw.githubusercontent.com/dwyl/english-words/master/words_alpha.txt';

  async function loadData() {
    try {
      let res = await fetch(english);
      let wordString = await res.text();
      let words = await buildWordsArray(wordString);

      let randomWords = getRandomWords(20, words);
      return randomWords.join(" ")
    } catch (e) {
      console.error(e);
    }
  }

  function getRandomInt(max) {
    return Math.floor(Math.random() * Math.floor(max));
  }

  function getRandomWord(words) {
    return words[getRandomInt(words.length)];
  }

  function getRandomWords(amount, words) {
    let result = [];

    for (let i = 0; i < amount; i++) {
      let randomWord = getRandomWord(words);
      result.push(randomWord);
    }

    return result;
  }

  async function buildWordsArray(wordString) {
    let result = [];
    let wordArray = wordString.split('\r\n');

    for (let i = 0; i < wordArray.length; i++) {
      if (wordArray[i].length < 7) {
        result.push(wordArray[i]);
      }
    }

    return result;
  }
 var test = loadData()
 console.log(test)
  export default {
    data() {
      console.log(this.wordList)
      return {
        wordList: this.wordList
      }
    },
    async mounted() {
      var words = await loadData()
      this.wordList = words
    }

  }
</script>

<style scoped>

</style>
