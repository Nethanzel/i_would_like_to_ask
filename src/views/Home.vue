<template>
  <div class="home">
    <p>
      Hola, soy <strong>Natanael Abad</strong>, estudiante de término de <strong>Ingeniería de Sistemas y Computación</strong> 
      de la universidad Dominicana O{{charOne}}M. Como parte de mi proyecto monografíco, me he propuesto realizar una 
      investigacion de caracter social, la que se basa en reconocer o identificar algunas de las razones que estan permitiendo 
      o que podrian permitir que las personas en nuestro país caigan como victima de filtración o robo de datos personales 
      (como contraseñas, datos bancarios o archivos privados) por parte de los archifamosos hackers.
    </p>

    <p>
      Actualmente, existe muy poca información de parte del estado sobre estadisticas o alguna otra información que pueda servir, por lo 
      que preferí crear mi propia fuente de referencia, pero para eso necesito que por favor, contestes algunas preguntas que he 
      creado para evaluar el desempeño de esta aplicación. <strong>No tendras que poner ningún dato personal, solo tus respuestas</strong>. 
      Si no tienes ningún desacuerdo y quieres contestarlas, presiona el link de abajo (donde dice continuar). Si no quieres hacerlo, solo 
      cierra la aplicación (o página) y listo.
    </p>

    <p>
      Tambien quiero que tengas claro que <strong>lo único que hace esta aplicación es reunir los datos que pongas como 
      respuestas</strong>. Podras ver tus respuestas, si por alguna razón quieres cambiar alguna respuesta, 
      cuando hayas contestado todo te dará la opción donde accedes a poder borrar alguna de ellas y luego volver a 
      contestarla. Tendras la opción de enviar tu cuestionario rellenado cuando quieras, luego que lo hayas enviado, ya no 
      podras volver a modificar nada.
    </p>

    <p>Si en algun momento notas que la aplicación funciona de forma incorrecta o te parece que es dificil de usar, tienes la 
      posibilidad de <router-link to="/report">enviar un reporte</router-link> cuando quieras, explicando lo que pasa o alguna 
      idea que quisieras compartirme. Podras ver un <router-link to="/overview">resumen</router-link> del progreso del proyecto.
    </p>

    <div id="nav" v-on:click="go()">
        <span id="goBtn" class="r_link">Continuar</span>
        <img id="spin" src="../assets/spin.png">
    </div>


  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  title: "I would like to ask...",
  data () {
    return {
      charOne: "&",
    }
  },

  methods: {
    go() {
      document.getElementById("spin").style.display = "block"
      document.getElementById("goBtn").style.display = "none"
      setTimeout(() => {
        this.clienttoken()
        this.goSurvey()
      }, 3000)
    },
    goSurvey() {
      let token = localStorage.getItem("auth")
      if(token != null) {
        this.$router.push({name: "Survey"})
      } else this.go()
    }
  },
}
</script>

<style scoped>
.home a {
    text-decoration: none;
    color: #79c471;
}

@keyframes rotate360 {

    to { transform: rotate(360deg); }
}

@-webkit-keyframes rotate360 {

    to { transform: rotate(360deg); }
}

#spin { 
    animation: 1.5s rotate360 infinite linear; 
    height: 40px;
    display: none;
}

@media only screen and (max-width: 750px) {
  .home {
    height: auto;
    cursor: default;
    padding-top: 9vh;

  }

  .home p {
    text-align: justify;
    padding: 10px 15px;
    font-size: 17px;
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
    color: #000;
  }
}
@media only screen and (min-width: 751px) {
  .home {
    height: auto;
    cursor: default;
    padding-top: 7vh;

  }

  .home p {
    text-align: justify;
    padding: 10px 20px;
    font-size: 19px;
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
    color: #000;
  }
  
}

</style>
