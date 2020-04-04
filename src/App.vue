<template>
  <div id="app">
    <AppHeader title="Welcome to Flag Search" />
    <country-search />
    <flag :country="country" />
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import CountrySearch from "./components/CountrySearch.vue";
import { eventBus } from './main';
import Flag from "./components/Flag.vue";

export default {
  name: "App",
  data: function() {
    return {
      country: 'gb'
    }
  },
  methods: {
    setCountryAlpha2Code: function(country) {
      fetch("https://restcountries.eu/rest/v2/name/" + country).then(res => {
        res.json().then(json =>  {
           this.country = json.map(e => e.alpha2Code)[0].toLowerCase()
        });
      });
    }
  },
  components: {
    AppHeader,
    CountrySearch,
    Flag
  },
  created: function() {
    var self = this;
    eventBus.$on('country-changed', (country) => {
      self.setCountryAlpha2Code(country);
    })
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
