<script>
export default {
  name: "Question",
  data: function () {
    return {
      progress: 66,
      currentQuestion: 0,
      question: {
        id: 1,
        title: "What is the disease?",
        answers: [
          {
            id: 1,
            title: "Cancer",
            isCorrect: true,
          },
          {
            id: 2,
            title: "Diabetes",
            isCorrect: false,
          },
          {
            id: 3,
            title: "Hypertension",
            isCorrect: false,
          },
          {
            id: 4,
            title: "Asthma",
            isCorrect: false,
          },
        ]
      },
    }
  }
}
</script>

<template>
  <v-container>
    <v-row
      align="center"
      justify="center"
    >
      <v-col cols="7">
        <v-progress-linear
          v-model="progress"
          height="10"
          rounded
        />
      </v-col>
      <v-col cols="6">
        <v-img src="@/assets/scan.jpg" />
      </v-col>
      <v-col
        v-for="n in 3"
        :key="n"
        cols="12"
        md="4"
      >
        <v-item v-slot="{active, toggle}">
          <v-card
            :color="active ? 'primary' : ''"
            class="d-flex align-center"
            dark
            height="200"
            @click="toggle"
          >
            <v-scroll-y-transition>
              <div
                v-if="active"
                class="text-h2 flex-grow-1 text-center"
              >
                Active
              </div>
            </v-scroll-y-transition>
          </v-card>
        </v-item>
      </v-col>
    </v-row>
  </v-container>
</template>


<style scoped>

</style>