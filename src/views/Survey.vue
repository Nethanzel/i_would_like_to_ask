<template>
  <div class="survey">
    <h1>Por favor conteste con honestidad</h1>

      <questions v-on:view="showView($event)" />

    <div id="nav" v-on:click="done()" v-if="finished">
        <span class="r_link">Finalizar</span>
    </div>

    <div id="superView">
      <img src="data:image/jpeg;base64,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" id="superView_img">
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
/*
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
*/
  methods: {
    done () {
      localStorage.setItem("iwouldliketoask", JSON.stringify({ stage: 1 }))
      this.$router.push("/done")
    },

    showView(uri) {
      document.getElementById("superView_img").src = uri
      let superView = document.getElementById("superView")
      superView.style.transform = "scale(1)"
    }
  },

  mounted () {
    let superView = document.getElementById("superView")

    superView.addEventListener("click", (e) => {
      let target = e.target.getAttribute("id")
      if(target == "superView") {superView.style.transform = "scale(0)"}
    })
  }
}
</script>

<style scoped>

#superView {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  background: #ffffff77;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  transform: scale(0);
  transition: transform .4s ease-in-out;
}




@media only screen and (max-width: 750px) {
  .survey {
    cursor: default;
    height: auto;
    padding-top: 11vh;
    padding-bottom: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;

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

  #superView_img {
    max-width: 87vh;
    min-width: 85vh;
     -moz-transform: rotate(90deg);
     -o-transform: rotate(90deg);
     -webkit-transform: rotate(90deg);
     transform: rotate(90deg);
  }

}

@media only screen and (min-width: 751px) {
  .survey {
    height: auto;
    padding-top: 10vh;
    padding-bottom: 15px;
    cursor: default;
    display: flex;
    flex-direction: column;
    align-items: center;
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

  #superView_img {
    max-width: 95vw;
    min-width: 90vw;
    max-height: 95vh;
  }
}

</style>
