<template>
    <div class="about">
        <img src="../assets/iWouldLike2.svg" alt="branding logo" id="logo">
        <h1><strong>I would like to ask...</strong></h1>

        <p>"I would to ask" o en español "Quisiera preguntar", es un pequeño proyecto de codigo abierto (Open Source), el cual 
          fue desarrollado por mi (<a href="https://facebook.com/natanaelabaad" target="_blank">Natanael Abad</a>) para poder reunir ciertos datos 
          sobre seguridad informatica que puedan ser usados como indicadores de la incidencia de eventos negativos a nivel de seguridad 
          informatica en Republica Dominicana.
        </p>

        <p>
          Mi intencion es mantener los datos publicos, a travez de esta misma aplicacion o por algun otro medio, ya que de nada 
          valdria mantenerlos escondidos cuando la razon de este proyecto es esa, al no haber fuentes confiables que dispongan 
          datos de forma publica, me fue necesario crear mi propia fuente de datos.
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