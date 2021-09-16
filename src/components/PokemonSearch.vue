<template>
  <div id="search">
    <b-form-input id="searchBar" v-model="text" placeholder="Enter your name"></b-form-input>
    <div class="mt-2">{{ text }}</div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        text: ''
      }
    }
  }
</script>