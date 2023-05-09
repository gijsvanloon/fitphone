<template>
  <div class="container">
    <div class="box">
      <h1>{{ header }}</h1>
      <p class="description">{{ description }}</p>
      <div>
        <p class="question">{{ question }}</p>
        <input type="number" placeholder="Aantal uur" v-model.number="hours">
        <input type="number" placeholder="Aantal minuten" v-model.number="minutes">
        <button @click="calculate">{{ button }}</button>
      </div>
    </div>
    <div class="results">
      <div v-if="showResults">
        <p class="resultsText">Je hebt een gemiddelde schermtijd van <span class="highlight">{{ hours }}</span> uur en <span class="highlight">{{ minutes }}</span> minuten per dag.</p>
        <p class="resultsText">Dat is <span class="highlight">{{ hoursWeekResult }}</span> uur en <span class="highlight">{{ minutesWeekResult }}</span> minuten per week.</p>
        <p class="resultsText">Dit zijn ongeveer <span class="highlight">{{ daysYearResult }}</span> dagen per jaar!</p>
        <p class="resultsText">Dat is ongeveer <span class="highlight">{{ lifeTimeResult }}</span> jaar in je hele leven constant naar je telefoon kijken!</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['header', 'description', 'question', 'button'],
  data() {
    return {
      hours: null,
      minutes: null,
      hoursWeekResult: null,  
      minutesWeekResult: null,
      daysYearResult: null,
      lifeTimeResult: null,
      showResults: false,
    }
  },
  methods: {
    calculate() {
      const dailyHours = this.hours;
      const dailyMinutes = this.minutes;

      const totalTimeInHours = dailyHours + Math.floor(dailyMinutes / 60);
      const totalTimeInMinutes = dailyMinutes % 60;

      const weeklyTimeInHours = totalTimeInHours * 7 + Math.floor(totalTimeInMinutes * 7 / 60);
      const weeklyTimeInMinutes = totalTimeInMinutes * 7 % 60;

      const yearlyTimeInHours = totalTimeInHours * 365 + Math.floor(totalTimeInMinutes * 365 / 60);
      const yearlyTimeInMinutes = totalTimeInMinutes * 365 % 60;
      const yearlyTimeInDays = Math.ceil(yearlyTimeInHours / 24);

      const lifeTime = Math.ceil(yearlyTimeInDays * 70 / 365);

      this.hoursWeekResult = weeklyTimeInHours;
      this.minutesWeekResult = weeklyTimeInMinutes;
      this.daysYearResult = yearlyTimeInDays;
      this.lifeTimeResult = lifeTime;

      this.showResults = true;
    }
  }
}
</script>

<style scoped>
h1 {
  font-size: 4rem;
  font-weight: 700;
  margin-bottom: 20px;
}

p {
  font-size: 1em;
  font-weight: 700;
}

.description {
  margin-bottom: 100px;
}

.question {
  color: #616161;
  margin-bottom: 20px;
}

input {
  padding: 1rem 0.5rem;
  border: none;
  background: #F3F3F3;
  color: black;
  border-radius: 100px;
  font-family: 'Manrope', sans-serif;
  text-align: center;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

input:focus {
  outline: none;
}

input::placeholder {
  color: #616161;
}

button {
  padding: 1rem 2rem;
  border: none;
  background: #FFAD76;
  color: black;
  border-radius: 100px;
  font-family: 'Manrope', sans-serif;
  text-align: center;
  margin-left: 10px;
}

button:hover {
  cursor: pointer;
  background: #E99D6A;
}

.container {
  align-items: center;
  height: 100vh;

  margin: 0 1rem;

  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-gap: 25px;
}

.box {
  grid-column: 2 / 6;
}

.results {
  grid-column: 7 / -2;
  background: #F3F3F3;
  padding: 50px;
  border-radius: 50px;
  height: 500px;
}

.resultsText {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 60px;
}

.highlight {
  color: #FFAD76;
  text-decoration: underline;
}

@media only screen and (max-width: 768px) {
  h1 {
    font-size: 2rem;
    font-weight: 700;
    margin-bottom: 20px;
  }

  p {
    font-size: 0.75em;
    font-weight: 700;
  }

  .description {
    margin-bottom: 50px;
  }

  .question {
    color: #616161;
    margin-bottom: 20px;
  }

  input {
    padding: 1rem 0.5rem;
    border: none;
    background: #F3F3F3;
    color: black;
    border-radius: 100px;
    font-family: 'Manrope', sans-serif;
    text-align: center;
    margin-bottom: 10px;
  }

  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }

  input:focus {
    outline: none;
  }

  input::placeholder {
    color: #616161;
  }

  button {
    padding: 1rem 2rem;
    border: none;
    background: #FFAD76;
    color: black;
    border-radius: 100px;
    font-family: 'Manrope', sans-serif;
    text-align: center;
    margin-left: 0px;
  }

  button:hover {
    cursor: pointer;
    background: #E99D6A;
  }

  .container {
    align-items: center;
    height: 100vh;

    margin: 0 2rem;

    display: grid;
    grid-template-columns: repeat(6, 1fr);
    grid-gap: 25px;
  }

  .box {
    grid-column: 1 / 4;
  }

  .results {
    grid-column: 4 / -1;
    background: #F3F3F3;
    padding: 25px;
    border-radius: 50px;
    height: 500px;
  }

  .resultsText {
    font-size: 1rem;
    font-weight: 700;
    margin-bottom: 30px;
  }

  .highlight {
    color: #FFAD76;
    text-decoration: underline;
  }
}

@media only screen and (max-width: 425px) {
  h1 {
    font-size: 2rem;
    font-weight: 700;
    margin-bottom: 20px;
  }

  p {
    font-size: 0.75em;
    font-weight: 700;
  }

  .description {
    margin-bottom: 50px;
  }

  .question {
    color: #616161;
    margin-bottom: 20px;
  }

  input {
    padding: 1rem 0.5rem;
    border: none;
    background: #F3F3F3;
    color: black;
    border-radius: 100px;
    font-family: 'Manrope', sans-serif;
    text-align: center;
    margin-bottom: 10px;
  }

  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }

  input:focus {
    outline: none;
  }

  input::placeholder {
    color: #616161;
  }

  button {
    padding: 1rem 2rem;
    border: none;
    background: #FFAD76;
    color: black;
    border-radius: 100px;
    font-family: 'Manrope', sans-serif;
    text-align: center;
    margin-left: 0px;
  }

  button:hover {
    cursor: pointer;
    background: #E99D6A;
  }

  .container {
    align-items: center;
    height: 100vh;

    margin: 0 2rem;

    display: grid;
    grid-template-columns: repeat(6, 1fr);
    grid-gap: 25px;
  }

  .box {
    grid-column: 1 / -1;
  }

  .results {
    grid-column: 1 / -1;
    background: #F3F3F3;
    padding: 25px;
    border-radius: 50px;
    height: 500px;
  }

  .resultsText {
    font-size: 1rem;
    font-weight: 700;
    margin-bottom: 30px;
  }

  .highlight {
    color: #FFAD76;
    text-decoration: underline;
  }
}
</style>