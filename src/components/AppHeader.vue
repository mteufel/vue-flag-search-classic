<template>
  <div>
    <h1>{{ title }}</h1>
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "AppHeader",
  props: {
    title: String
  }
};
</script>