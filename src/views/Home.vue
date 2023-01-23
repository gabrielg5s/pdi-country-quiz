<template>
  <div>
      <select
      v-model="countrySelect"
      @change="getCountryFlag()"
    >
      <option v-for="country in listCountries" :key="country.name" :value="country.name" :test="country.name">{{ country.name }}</option>
    </select>
  </div>  
<br>
  <div >
      <img v-if="descriptionCountry" alt="Country Flag" :src="'' + descriptionCountry[0].flags.png"/>
  </div>
  {{ listCountries }}  
  
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

  created(){
    this.getCountryNames();
  },

  methods: {

   async getCountryNames(){
      const response = await axios.get("https://restcountries.com/v3.1/all")
             
      this.listCountries = response.data.map((country) => {
          const countryDetail ={
            name: country.name.common,
            capital: country.capital,
            flags: country.flags.png,
          }
          return countryDetail
        });
    },

  async getCountryFlag(){
    const response = await axios.get(`https://restcountries.com/v3.1/name/${this.countrySelect}`)
    this.descriptionCountry = response.data
  }
  }

}
</script>
