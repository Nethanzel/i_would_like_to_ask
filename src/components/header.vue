<template>
  <div class="header">
    <img src="../assets/iWouldLike2.svg" alt="branding" id="branding">

    <div id="headerBtns">

      <router-link to="/about" class="link">
        <div class="icon">
          <img src="../assets/info.svg" alt="info" id="info"> 
          <span class="tag"> Saber mas</span>
        </div>
      </router-link>

      <router-link to="/report" class="link">
        <div class="icon">
          <img src="../assets/problem.svg" alt="problem" id="prob"> 
          <span class="tag"> Reportar fallo</span>
        </div>
      </router-link>
    </div>

  </div>
</template>

<style>

.link {
  text-decoration: none;
}

@media only screen and (max-width: 750px) {
  .header {
    width: 100vw;
    height: 9vh;
    box-shadow: 0 7px 8px rgba(0, 0, 0, 0.658);
    position: fixed;
    top: 0;
    background: #474747;

    display: flex;
  }

  #headerBtns {
    display: flex;
    width: 100%;
    justify-content: flex-end;
    margin-top: auto;
    margin-bottom: auto;
  }

  #branding {
    height: 8.5vh;
    margin-top: 3px;
    margin-left: 3px;
    align-self: flex-start;
    display: inline-block;
  }

  .icon {
    align-self: flex-end;
    position: relative;
    margin-right: 5px;
    width: auto;
    display: flex;
    align-items: center;
    padding: 5px 10px;

  } 
  
  #info {
    max-height: 25px;
    height: auto;
    align-self: flex-end;
    display: inline-block;
    border-radius: 50%;
  }

  #prob {
    max-height: 25px;
    height: auto;
    align-self: flex-end;
    display: inline-block;
    border-radius: 50%;
  }

  .icon:hover #prob {
    background: #c47171;
  }

  .icon:hover #info {
    background: #79c471;
  }

  .icon:hover {
    border-bottom-left-radius: 5px;
    border-top-left-radius: 5px;
    border-bottom-right-radius: 5px;
    border-top-right-radius: 5px;
    background: #696969;
  }

  .tag {
    display: none;
  }
}

@media only screen and (min-width: 751px) {
  .header {
    height: 7vh;
    width: 100vw;
    box-shadow: 0 7px 8px rgba(0, 0, 0, 0.658);
    position: fixed;
    top: 0;
    background: #474747;
    display: flex;

  }

  #headerBtns {
    display: flex;
    width: 100%;
    justify-content: flex-end;
    margin-top: auto;
    margin-bottom: auto;
  }

  #branding {
    height: 6.5vh;
    margin-top: 3px;
    margin-left: 3px;
    align-self: flex-start;
    display: inline-block;
  }

  .icon {
    align-self: flex-end;
    position: relative;
    margin-right: 5px;
    width: auto;
    display: flex;
    align-items: center;
    padding: 5px 5px;

  } 
  
  #info {
    max-height: 25px;
    height: auto;
    align-self: flex-end;
    display: inline-block;
    border-radius: 50%;
  }

  #prob {
    max-height: 25px;
    height: auto;
    align-self: flex-end;
    display: inline-block;
    border-radius: 50%;
  }

  .icon:hover #prob {
    background: #c47171;
  }

  .icon:hover #info {
    background: #79c471;
  }

  .icon:hover {
    border-bottom-left-radius: 5px;
    border-top-left-radius: 5px;
    border-bottom-right-radius: 5px;
    border-top-right-radius: 5px;
    background: #696969;
  }

  .tag {
    color: #fff;
    display: inline-block;
    margin-left: 5px;
    font-size: 14px;
  }
}


</style>
