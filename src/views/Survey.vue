<template>
  <div class="survey">
    <h1>Por favor conteste con honestidad</h1>

      <questions />

    <div id="nav" v-on:click="done()" v-if="finished">
        <span class="r_link">Finalizar</span>
    </div>

  </div>
</template>

<script>

import questions from '@/components/Questions.vue'

export default {
  name: "survey",
  title: "I would like to ask...",

  components: {
    questions
  },

  data() {
    return {
      finished: false
    }
  },

  beforeCreate() {
    let status = localStorage.getItem("iwouldliketoask")
    if(status == null) {
      this.$router.push("/")
    } else {

      status = JSON.parse(status)
      if(status.stage == 1) {
        this.$router.push("/done")
      }
    }
  },

  methods: {
    done () {
      localStorage.setItem("iwouldliketoask", JSON.stringify({ stage: 1 }))
      this.$router.push("/done")
    }
  }
}
</script>

<style scoped>

@media only screen and (max-width: 750px) {
  .survey {
    cursor: default;
    padding-top: 9.5vh;
    height: 90.5vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-top: -9vh;
  }

  h1 {
    text-align: center;
    margin: 0 10px;
  }

  #nav {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 30px 0 30px 0;
  }

  #nav .r_link {
    background: #79c471;
    padding: 10px 20px;
    border-bottom-left-radius: 5px;
    border-top-left-radius: 5px;
    border-bottom-right-radius: 5px;
    border-top-right-radius: 5px;
    text-decoration: none;
    font-size: 17px;
  }

  #nav .r_link:hover {
    background: #53ff78;
    color: #000
  }

}

@media only screen and (min-width: 751px) {
  .survey {
    height: 92.5vh;
    cursor: default;
    padding-top: 7.5vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-top: -7vh;
  }

  h1 {
    text-align: center;
    margin: 0 10px;
  }

  #nav {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 30px 0 30px 0;
  }

  #nav .r_link {
    background: #79c471;
    padding: 10px 20px;
    border-bottom-left-radius: 5px;
    border-top-left-radius: 5px;
    border-bottom-right-radius: 5px;
    border-top-right-radius: 5px;
    text-decoration: none;
    font-size: 19px;
  }

    #nav .r_link:hover {
    background: #53ff78;
    color: #000
  }
}

</style>
