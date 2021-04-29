<template>
  <div class="mainContent">
    <div v-for="item in covid_cases" :key="item.abbreviation">
      <vs-card>
        <template #title>
          <h3>{{ item.country }}</h3>
        </template>

        <template #text>
          <div>population: {{ item.population }}</div>
          <div>Confirmed: {{ item.confirmed }}</div>
          <div>Deaths: {{ item.deaths }}</div>
        </template>
        <template #interactions>
          <vs-button danger icon>
            <i class="bx bx-heart"></i>
          </vs-button>
          <vs-button class="btn-chat" shadow primary>
            <i class="bx bx-chat"></i>
            <span class="span"> {{ item.population }} </span>
          </vs-button>
        </template>
      </vs-card>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      covid_cases: [],
      country: '',
    }
  },
  async fetch() {
    this.getCountry()
    const API = `https://covid-api.mmediagroup.fr/v1/cases?country=${this.country}`

    this.covid_cases = await fetch(API).then((res) => res.json())
  },
  methods: {
    getCountry() {
      const slug = this.$route.params.slug
      this.country = slug
    },
  },
}
</script>
<style scoped></style>
