<template>
  <div id="header">
    <h1>{{ header }}</h1>
  </div>
</template>

<script>
  export default {
    name: "Header",
    data() {
      return {
        header: "Simple Recipe App",
      }
    },
  }
</script>

<style lang="scss">
  @import "../scss/variables.scss";
  @import "../scss/mixins.scss";
  #header h1 {
    @include defaultText();
    color:$highlight;
    font-weight: bold;
    font-size: 28px;
    text-align: center;
    margin-bottom:30px;
  }
</style>