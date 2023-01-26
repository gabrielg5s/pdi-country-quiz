<template>
  <section class="content">
    <div class="App">
      <div class="titleQuiz">
        <h1>Country Quiz</h1>
      </div>
      <div class="boxQuiz">
        <img class="adventureImage" src="../assets/images/undraw_adventure_4hum.svg" />
        <div class="quizModetitle">
          <h2>Escolha o modo do quiz</h2>
        </div>
        <!-- <div>
                          <select v-model="countrySelect" @change="getCountryFlag()">
                            <option v-for="country in listCountries" :key="country.name" :value="country.name" :test="country.name">{{
                              country.name
                            }}</option>
                          </select>
                        </div> -->
        <div>
          <img v-if="descriptionCountry" alt="Country Flag" :src="'' + descriptionCountry[0].flags.png" />
        </div>
      </div>
      <footer>
        <div class="footer-content">
          <p>created by @gecinco - devChallenges.io</p>
        </div>
      </footer>
    </div>
  </section>
</template>

<script>
import axios from 'axios'


export default {
  name: 'HomeView',
  data() {
    return {
      descriptionCountry: "",
      countrySelect: "",
      listCountries: [],
    }
  },

  created() {
    this.getCountryNames();
  },

  methods: {

    async getCountryNames() {
      const response = await axios.get("https://restcountries.com/v3.1/all")

      this.listCountries = response.data.map((country) => {
        const countryDetail = {
          name: country.name.common,
          capital: country.capital,
          flags: country.flags.png,
        }
        return countryDetail
      });
    },

    async getCountryFlag() {
      const response = await axios.get(`https://restcountries.com/v3.1/name/${this.countrySelect}`)
      this.descriptionCountry = response.data
    }
  }

}
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&family=Poppins:wght@400;700&display=swap');


.App {
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
  justify-content: center;
}

.titleQuiz {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  width: 464px;
  margin-bottom: 10px;
}

.boxQuiz .adventureImage {
  position: absolute;
  right: 0;
  top: -4.6875em;
}

h2 {
  font-family: 'Poppins';
  font-weight: 700;
  color: #2F527B;
  margin-top: 52px;
  font-size: 24px;
}

.quizModetitle {
  padding: 15px 0;
  display: flex;
  justify-content: center;
}

h1 {
  font-family: 'Poppins', sans-serif;
  color: #F2F2F2;
  text-transform: uppercase;
  font-size: 36px;
  margin-bottom: 0;
}

body {
  background-image: url("../assets/images/background.png");
  background-size: auto;
  background-repeat: no-repeat;
}

.boxQuiz {
  background-color: #FFFFFF;
  width: 464px;
  height: 515px;
  border-radius: 24px;
  box-sizing: border-box;
  position: relative;
}

.content {
  display: flex;
flex-direction: row;
justify-content: center;
align-items: center;
}

.footer-content {
  font-family: 'Montserrat', sans-serif;
  color: #F2F2F2;
  display: flex;
  align-items: flex-end;
  justify-content: center;
}
</style>
