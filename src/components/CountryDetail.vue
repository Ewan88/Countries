<template lang="html">
  <div v-if="country">
    <h2>{{ country.name }}</h2>
    <p>{{ country.capital }}</p>
    <p>{{ country.population }}</p>
    <p v-for="(language, index) in country.languages">{{ language.name }}</p>
    <img :src="country.flag" />
  </div>
</template>

<script>
export default {
  name: "country-detail",
  props: ["country"]
}
</script>

<style lang="css" scoped>

img {
  width: 300px;
  height: auto;
}
</style>
