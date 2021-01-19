<template>
    <div class="about">
        <img src="../assets/iWouldLike2.svg" alt="branding logo" id="logo">
        <h1><strong>I would like to ask... (Quisiera preguntar...)</strong></h1>
    </div>
</template>

<style scoped>

@media only screen and (max-width: 750px) {
  .about {
    height: auto;
    cursor: default;
    padding-top: 9.5vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

}

@media only screen and (min-width: 751px) {
  .about {
    height: auto;
    cursor: default;
    margin: 0 10px 15px 10px;
    padding-top: 7.5vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  #logo {
    height: 250px;
  }

  h1 {
    text-align: center;
  }
}


</style>