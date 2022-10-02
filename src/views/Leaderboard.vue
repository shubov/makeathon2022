<script>
export default {
  name: "Leaderboard",
  data: function () {
    return {
      headers: [
        { text: 'Place', value: 'place', width: '10%'},
        {
          text: 'Student',
          align: 'start',
          sortable: false,
          value: 'name',
        },
        { text: 'Questions Answered', value: 'questions_answered' },
        { text: '% Correct', value: 'overall_correct' },
      ],
      students: [
        {
          place: 2,
          name: 'Rita',
          overall_correct: 86,
          questions_answered: 25,
        },
        {
          place: 4,
          name: 'Mike',
          overall_correct: 76,
          questions_answered: 35,
        },
        {
          place: 5,
          name: 'Clark',
          overall_correct: 32,
          questions_answered: 50,
        },
        {
          place: 1,
          name: 'Yana',
          overall_correct: 91,
          questions_answered: 23,
        },
        {
          place: 3,
          name: 'Suzanne',
          overall_correct: 83,
          questions_answered: 42,
        }
      ],
    }
  }
}
</script>

<template>
  <v-container>
    <v-row
      justify="center"
      align="center"
    >
      <v-col
        cols="12"
        class="text-center"
      >
        <p 
          class="text-h2 font-weight-bold primary--text"
        >
          Score Board
        </p>
      </v-col>
      <v-col cols="12">
        <v-data-table
          :headers="headers"
          :items="students"
          :sort-by="['place']"
          class="elevation-1"
        />
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped>

</style>