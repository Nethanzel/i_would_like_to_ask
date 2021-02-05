<template>
    <div class="about">
        <img src="../assets/iWouldLike2.svg" alt="branding logo" id="logo">
        <h1><strong>I would like to ask...</strong></h1>

        <p>"I would to ask" o en español "Quisiera preguntar", es un pequeño proyecto de código abierto (Open Source), el cual 
          fue desarrollado para realizar una investigación y reunir datos sobre el contexto de seguridad informática que permitan 
          detectar indicadores de la incidencia de eventos negativos en el area en República Dominicana.
        </p>

        <p>
          La intención es mantener los datos accesibles a todos, a travez de esta misma aplicacion o por algún otro medio, ya que de nada 
          valdria mantenerlos escondidos cuando la razon de este proyecto se basa en que al no haber fuentes confiables que dispongan 
          datos de forma pública, es necesario realizar una investigación y crear una fuente de datos.
        </p>

        <p>
          Puedes accerder al <a href="https://github.com/Nethanzel/i_would_like_to_ask" target="_blank">repositorio del proyecto</a> en Github y colaborar o ver 
          los códigos fuente, cualquier idea/critica será bien recibida.
        </p>
    </div>
</template>

<style scoped>

.about a {
    text-decoration: none;
    color: #79c471;
}


@media only screen and (max-width: 750px) {
  .about {
    height: auto;
    cursor: default;
    padding-top: 10vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  #logo {
    height: 175px;
  }

  h1 {
    text-align: center;
    margin: 0 10px 15px 10px;
  }

  p {
    margin: 0 10px 15px 10px;
    font-size: 17px;
    text-align: justify;
  }

}

@media only screen and (min-width: 751px) {
  .about {
    height: auto;
    cursor: default;
    margin: 0 10px 15px 10px;
    padding-top: 8vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    min-width: 350px;
  }

  #logo {
    height: 250px;
  }

  h1 {
    text-align: center;
    margin: 0 10px 15px 10px;
  }

  p {
    margin: 0 10px 15px 10px;
    font-size: 19px;
    text-align: justify;
  }
}


</style>