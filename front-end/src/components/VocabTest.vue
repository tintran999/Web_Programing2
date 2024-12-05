<template>
    <div>
      <h2>Score: {{ score }} out of {{ this.words.length * 2 }}</h2> <!-- Adjust the total score to account for multiple translations -->
  
      <form action="#" @submit.prevent="onSubmit">
        <div class="ui labeled input fluid">
          <div class="ui label">
            <i class="germany flag"></i> German
          </div>
          <input type="text" readonly :disabled="testOver" :value="currWord.german"/>
        </div>
        <div class="ui labeled input fluid">
          <div class="ui label">
            <i class="united kingdom flag"></i> English
          </div>
          <input type="text" placeholder="Enter word in English..." v-model="english" :disabled="testOver" autocomplete="off" />
        </div>
        <div class="ui labeled input fluid">
          <div class="ui label">
            <i class="vietnam flag"></i> Vietnam
          </div>
          <input type="text" placeholder="Enter word in Vietnamese..." v-model="vietnamese" :disabled="testOver" autocomplete="off" />
        </div>
        <button class="positive ui button" :disabled="testOver">Submit</button>
      </form>
  
      <p :class="['results', resultClass]">
        <span v-html="result"></span>
      </p>
    </div>
  </template>
  
  
  <script>
export default {
  name: 'vocab-test',
  props: {
    words: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      randWords: [...this.words.sort(() => 0.5 - Math.random())],
      incorrectGuesses: [],
      result: '',
      resultClass: '',
      english: '',
      vietnamese: '',
      score: 0,
      testOver: false
    };
  },
  computed: {
    currWord() {
      return this.randWords.length ? this.randWords[0] : '';
    }
  },
  methods: {
    onSubmit() {
      let correct = 0;

      if (this.english === this.currWord.english) {
        correct++;
      } else {
        this.incorrectGuesses.push(this.currWord.german);
      }

      if (this.vietnamese === this.currWord.vietnam) {
        correct++;
      } else {
        this.incorrectGuesses.push(this.currWord.vietnam);
      }

      this.flash(correct === 2 ? 'Correct!' : 'Wrong!', correct === 2 ? 'success' : 'error', { timeout: 1000 });
      this.score += correct;

      this.english = '';
      this.vietnamese = '';
      this.randWords.shift();

      if (this.randWords.length === 0) {
        this.testOver = true;
        this.displayResults();
      }
    },
    displayResults() {
      if (this.incorrectGuesses.length === 0) {
        this.result = 'You got everything correct. Well done!';
        this.resultClass = 'success';
      } else {
        const incorrect = this.incorrectGuesses.join(', ');
        this.result = `<strong>You got the following words wrong:</strong> ${incorrect}`;
        this.resultClass = 'error';
      }
    }
  }
};
</script>

  
  <style scoped>
  .results {
    margin: 25px auto;
    padding: 15px;
    border-radius: 5px;
  }
  
  .error {
    border: 1px solid #ebccd1;
    color: #a94442;
    background-color: #f2dede;
  }
  
  .success {
    border: 1px solid #d6e9c6;
    color: #3c763d;
    background-color: #dff0d8;
  }
  </style>