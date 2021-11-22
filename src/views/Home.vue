<template>
  <div class="home">
    <h1>TEST QUIZ</h1>
    <div style="width: 50%; margin: 0 auto;">
      <div v-if="index < count">
        <p>{{ questions[index]['question'] }}</p>
        <label :for="key" style="display: block; border: 1px solid #000; padding: 1rem;"
          v-for="(answer, key) in questions[index]['answers']" :key="key"
        >
          <input 
            type="radio" 
            :id="key" style="visibility: hidden;" 
            :value="key" 
            @click="answered($event)"
            v-model="selectedAnswer"
          />
          {{ answer }}
        </label>
      </div>
      <div v-else>
        <h2>Results</h2>
          <div>

          </div>
        <!-- <div v-if="answerArr[0] == 'a' && answerArr[1] == 'a' && answerArr[2] == 'a' && answerArr[3] == 'a'">
          <h1>Option 1</h1>
          <a href="https://www.kerastase.ca/en/collections/ge nesis/genesis-oily-weakened-hair-care- set.html">ACCESS YOUR EXCLUSIVE OFFER</a>
        </div>
        <div v-else-if="answerArr[0] == 'a' && answerArr[1] == 'a' && answerArr[2] == 'a' && answerArr[3] == 'b'">
          <h1>Option 2</h1>
          <a href="https://www.kerastase.ca/en/collections/ge nesis/genesis-oily-weakened-hair-care- set.html">ACCESS YOUR EXCLUSIVE OFFER</a>
        </div>
        <div v-else-if="answerArr[0] == 'a' && answerArr[1] == 'a' && answerArr[2] == 'b' && answerArr[3] == 'a'">
          <h1>Option 3</h1>
          <a href="https://www.kerastase.ca/en/collections/ge nesis/genesis-oily-weakened-hair-care- set.html">ACCESS YOUR EXCLUSIVE OFFER</a>
        </div>
        <div v-else-if="answerArr[0] == 'a' && answerArr[1] == 'a' && answerArr[2] == 'b' && answerArr[3] == 'b'">
          <h1>Option 4</h1>
          <a href="https://www.kerastase.ca/en/collections/ge nesis/genesis-oily-weakened-hair-care- set.html">ACCESS YOUR EXCLUSIVE OFFER</a>
        </div>
        <div v-else-if="answerArr[0] == 'b' || answerArr[1] == 'b'">
          <h1>Option 5</h1>
          <a href="https://www.kerastase.ca/en/collections/ge nesis/genesis-oily-weakened-hair-care- set.html">ACCESS YOUR EXCLUSIVE OFFER</a>
        </div> -->
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  data() {
    return {
      index: 0,
      selectedAnswer: '',
      answerArr: [],
      count: 4,
      option: '',
      questions: [
        {
          question: "Do you see hair strands in the shower, around the house, everywhere you go?",
          answers: {
            a: "yes",
            b: "no"
          }
        },
        {
          question: "Have you noticed an increase in hair fall this season?",
          answers: {
            a: "yes",
            b: "no"
          }
        },
        {
          question: "Which of the below best describes your hair?",
          answers: {
            a: "Greasy Roots",
            b: "Dry"
          }
        },
        {
          question: "Which of the below best describes your hair?",
          answers: {
            a: "Normal to Thin",
            b: "Thick"
          }
        }
      ],
      results: [
        {
          option: "Option 1",
          resultCombo: ['a','a','a','a'],
          link: 'www.google.com'
        },
        {
          option: "Option 2",
          resultCombo: ['a','a','a','b'],
          link: 'www.google.com'
        },
        {
          option: "Option 3",
          resultCombo: ['a','a','b','a'],
          link: 'www.google.com'
        },
        {
          option: "Option 4",
          resultCombo: ['a','a','b','b'],
          link: 'www.google.com'
        },
        {
          option: "Option 5",
          resultCombo: null,
          link: 'www.google.com'
        },
      ],
    }
  },
  methods: {
    answered(e) {
      this.selectedAnswer = e.target.value
      this.answerArr.push(this.selectedAnswer)
      this.nextQuestion()
      this.findDeal()
      console.log(this.answerArr)
    },
    nextQuestion() {
        this.index++
        this.selectedAnswer = ''
    },
    showResults() {
        this.index++
    },
    findDeal() {
      // using .some because it doesn't continue iterating once it returns a true value
      // This might need to be state. 
      // using .some because it doesn't continue iterating once it returns a true value
      this.results.some((result, idx) => {
        // This console log is checking to see if the .some method still runs after it finds a result
        console.log('This is running! ' + idx)
        if(this.answerArr[0] === 'b' && this.answerArr[1] === 'b') {
          this.option = this.results[4] 
          return true // this is to stop the .some method
        } else if(result.resultCombo.every((char, idx) => char === this.answerArr[idx]) ) {
          this.option = result // set the result to state or some variable
          return true // this is to stop the .some method
        } else {
          this.option = 'Something went wrong'
        }
      })
      return this.option
      // results.some(result => {
      //   if (result.resultCombo.every(function(elem, idx) {
      //     elem === answerArr[idx]
      //   })) {

      //   }
      // })
      // if (this.index == this.count) {
      //   for (let i = 0; i < combos.length; i++) {
      //     console.log(combos[i])
      //     if (combos[i] === this.answerArr) {
      //       console.log('yes')
      //     }
      //   }
      // }
    }
  },
};
</script>
