<template>
  <div id="app">
    <headeR />
    <router-view />
  </div>
</template>

<script>
import headeR from '@/components/header.vue'

export default {
  title: "I would like to ask...",
  components: {
    headeR
  },

}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Raleway:wght@200&display=swap');

* {
  margin: 0;
  padding: 0;
  font-family: 'Raleway', sans-serif;
}

body {
  background: linear-gradient(#577357, #575757) fixed;
  background-repeat: no-repeat;
  background-size: auto;
  color: #ffffff;
  max-width: 1366px;
  margin-left: auto;
  margin-right: auto;
}

p {
  cursor: default;
}
</style>