<template lang="html">
  <div class="">
    <select v-model="selectedCountry" v-on:change="handleSelect">
      <list-item v-for="(country, index) in countries" :key="index" :country="country" />
    </select>
  </div>
</template>

<script>

import ListItem from './ListItem.vue';
import { eventBus } from '../main.js';

export default {
  data (){
    return {
      selectedCountry: null
    }
  },
  name: "countries-list",
  props: ["countries"],
  components: {
    "list-item": ListItem
  },
  methods: {
    handleSelect(){
      eventBus.$emit('country-selected', this.selectedCountry);
    }
  }
}
</script>

<style lang="css" scoped>
</style>
