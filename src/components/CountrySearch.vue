<template>
  <div>
     <a-select class="country-search"
      show-search
      placeholder="search for a country here"
      :show-arrow="false"
      :options="options"
      @search="onSearch"
      @select="onSelection"
      v-model:value="value1"
      :filter-option="false" >
      <template v-if="fetching" #notFoundContent>
            <a-spin size="small" />
      </template>
     </a-select>

  </div>
  
</template>

<script>

export default {
  name: "CountrySearch",
  components: {
  //  vSelect
  },
  data: function() {
    return {
      fetching: false,
      options: [],
      value1: []
    };
  },
  methods: {
    onFocus() {
      console.log('Focus')
    },
    onSelection(value, option) {
      console.log('onSelection: ', { value, option })
      console.log('onSelection: ', this.value1)
      this.$parent.$emit('countryChanged', this.value1.toLowerCase());
    },
    onSearch(search) {
      console.log('onSearch ', search)
      this.search(search);
    },
    search(search) {
      if (search === "") {
        return;
      }
      this.fetching = true
      fetch("https://restcountries.com/v2/name/" + search).then(res => {
        res.json().then(json => { 
          this.options = json.map(e => ( { label: e.name, value: e.alpha2Code } ) )
          this.fetching = false
          console.log(this.options)
        });
      });
    }
  }
};
</script>

<style>
.country-search {
  display: block;
  text-align: left;
  margin-left: auto;
  margin-right: auto;
  width: 400px;
}
</style>