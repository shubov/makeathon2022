<script>
export default {
  name: "Question",
  data: function () {
    return {
      showResults: false,
      disableButtons: false,
      currentQuestionID: 0,
      colors: ['primary', 'secondary', 'success', 'warning', 'info'],
      questions: [{
        scan: 1,
        heatmap: 0,
        age: 25,
        sex: "Female",
        title: "What is the disease?",
        answers: [
          {
            title: "Pneumothorax",
            isCorrect: true,
          },
          {
            title: "Atelectasis",
            isCorrect: false,
          },
          {
            title: "Pneumonia",
            isCorrect: false,
          },
          {
            title: "Consolidation",
            isCorrect: false,
          },
        ]
      },
      {
        scan: 2,
        heatmap: 0,
        age: 30,
        sex: "Male",
        title: "What is the disease?",
        answers: [
          {
            title: "Edema",
            isCorrect: true,
          },
          {
            title: "Lung Opacity",
            isCorrect: false,
          },
          {
            title: "Lung Lesion",
            isCorrect: false,
          },
          {
            title: "No Finding",
            isCorrect: false,
          },
        ]
      }],
      correctAnswers: 0,
    }
  },
  computed: {
    currentQuestion() {
      return this.questions[this.currentQuestionID]
    },
    totalNumberOfQuestions() {
      return this.questions.length
    },
    percentage() {
      return Math.round((this.currentQuestionID + 1) / (this.totalNumberOfQuestions + 1) * 100)
    },
    currentAnswers() {
      return this.currentQuestion.answers.slice().sort(() => (Math.random() > .5) ? 1 : -1)
    },
    currentScan() {
      return this.currentQuestion.scan
    },
    currentTitle() {
      return this.currentQuestion.title
    },
    currentImage() {
      return require(this.currentScan)
    },
    currentGender() {
      return this.currentQuestion.sex
    },
    currentAge() {
      return this.currentQuestion.age
    },
    results() {
      return this.correctAnswers / this.totalNumberOfQuestions * 100
    },
    resultClass() {
      if (this.results < 50) {
        return 'error'
      } else if (this.results < 75) {
        return 'warning'
      } else {
        return 'success'
      }
    }
  },
  methods: {
    nextQuestion() {
      this.currentQuestionID++
    },
    previousQuestion() {
      this.currentQuestionID--
    },
    selectAnswer(isCorrect) {
      this.disableButtons = true
      if (isCorrect) {
        this.correctAnswers++
      }
      setTimeout(() => {
        this.disableButtons = false
        if (this.currentQuestionID < this.totalNumberOfQuestions - 1) {
          this.nextQuestion()
        } else {
          this.showResults = true
        }
      }, 1000)
    },
  },
}
</script>

<template>
  <div
    v-if="showResults"
    class="d-flex align-center justify-center loader--full"
    :class="resultClass"
  >
    <div class="d-flex flex-column align-center justify-center">
      <p class="text-h1 font-weight-bold white--text">
        {{ correctAnswers }} / {{ totalNumberOfQuestions }}
      </p>
      <p class="text-h5 font-weight-bold white--text">
        {{ correctAnswers / totalNumberOfQuestions * 100 }}% of the questions were answered correctly
      </p>
      <v-btn
        rounded
        depressed
        to="/leaderboard"
      >
        see the leaderboard
      </v-btn>
    </div>
  </div>
  <v-container
    v-else
    style="min-height: 100%"
  >
    <template>
      <v-row
        v-if="currentQuestion"
        align="center"
        justify="center"
      >
        <v-col cols="7">
          <v-progress-linear
            v-model="percentage"
            height="10"
            rounded
          />
        </v-col>
        <v-col cols="6">
          <v-fade-transition mode="out-in">
            <v-img
              :key="currentScan + '' + currentQuestionID + Math.random() * 100"
              :src="require(`@/assets/images/${currentScan}.jpg`)"
            />
          </v-fade-transition>
        </v-col>
        <v-col cols="12">
          <p class="text-subtitle text-center pb-0 mb-0">
            {{ currentGender }}, {{ currentAge }}
          </p>
          <p class="text-h5 text-center">
            {{ currentTitle }}
          </p>
        </v-col>
        <v-col
          v-for="({title,isCorrect}, index) in currentAnswers"
          :key="index + '' + currentQuestionID"
          cols="12"
          sm="6"
          md="4"
          lg="3"
        >
          <v-item>
            <v-card
              :color="colors[index]"
              class="d-flex align-center justify-center font-weight-bold text-h6"
              dark
              :elevation="disableButtons ? 0 : 10"
              :disabled="disableButtons"
              :style="disableButtons ? 'pointer-events: none' : ''"
              height="150"
              @click="selectAnswer(isCorrect)"
            >
              {{ title }}
            </v-card>
          </v-item>
        </v-col>
        <v-col
          v-if="false"
          cols="12"
          class="d-flex justify-center"
        >
          <v-btn
            color="primary"
            class="mx-auto"
            x-large
            @click="nextQuestion"
          >
            Next
          </v-btn>
        </v-col>
      </v-row>
      <div
        v-else
        class="d-flex align-center justify-center loader"
      >
        <v-progress-circular
          indeterminate
          color="primary"
          size="64"
          class="d-block"
        />
      </div>
    </template>
  </v-container>
</template>


<style scoped lang="scss">
.loader {
  height: calc(100vh - 24px);
  &--full {
    height: 100vh !important;
  }
  width: 100%;
}

</style>