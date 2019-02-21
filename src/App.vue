<template lang="html">
  <div>
    <h1>Countries</h1>
    <div class="main-container">
      <input v-model="input" v-on:change="findCountry"></input>
      <countries-list :countries="countries" />
      <country-detail :country="selectedCountry" />
    </div>
  </div>
</template>

<script>

import CountriesList from './components/CountriesList.vue';
import CountryDetail from './components/CountryDetail.vue';
import { eventBus } from './main.js';

export default {
  data(){
    return {
      countries: [],
      selectedCountry: null,
      input: ''
    }
  },
  components: {
    "countries-list": CountriesList,
    "country-detail": CountryDetail
  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
    .then(res => res.json())
    .then(countries => this.countries = countries)

    eventBus.$on('country-selected', (country) => {
      this.selectedCountry = country;
    });
  },
  methods: {
    findCountry(){
      let a = [];
      for (let i = 0; i < this.countries.length; i++){
        if (this.countries[i].name.toLowerCase().includes(this.input.toLowerCase())){
          a.push(this.countries[i]);
        };
      };
      if (a.length){
        this.selectedCountry = a[0];
      };
    }
  }
}
</script>

<style lang="css" scoped>
  .main-container {
    display: flex;
    justify-content: space-between;
    flex-direction: column;
  }
</style>
