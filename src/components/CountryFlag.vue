<template>
  <div>
    <img id="flag-image" border="0" src="../assets/blank.gif" v-bind:class="flagCss" />
  </div>
</template>

<script>
export default {
  name: "Flag",
  props: {
    country: String
  },
  computed: {
    flagCss: function() {
      return "flag flag-" + this.country;
    }
  }
};
</script>


<style scoped src="@/assets/flags.css">
</style>