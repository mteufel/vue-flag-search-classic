<template>
  <div>
    <v-select
      class="country-search"
      v-model="selected"
      :options="options"
      @input="onSelection"
      @search="onSearch"
    />
  </div>
  
</template>

<script>
import vSelect from "vue-select";
import { eventBus } from '../main'
import "vue-select/dist/vue-select.css";

export default {
  name: "CountrySearch",
  components: {
    vSelect
  },
  data: function() {
    return {
      options: [],
      selected: ""
    };
  },
  methods: {
    onSelection(value) {
      eventBus.$emit('country-changed', value)
    },
    onSearch(search) {
      this.search(search);
    },
    search(search) {
      if (search === "") {
        return;
      }
      fetch("https://restcountries.eu/rest/v2/name/" + search).then(res => {
        res.json().then(json => (this.options = json.map(e => e.name)));
      });
    }
  }
};
</script>

<style>
.country-search {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 400px;
}
</style>