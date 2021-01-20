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
/*
  beforeCreate() {
    let status = localStorage.getItem("iwouldliketoask")

    if(status != null) {
      status = JSON.parse(status)

      if(status.stage == 0) {
        this.$router.push("/survey")
      } else if(status.stage ==1) {
        this.$router.push("/done")
      }
    }
  }
*/

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
  background-color: #575757;
  color: #ffffff;
  max-width: 1366px;
  margin-left: auto;
  margin-right: auto;
}
</style>