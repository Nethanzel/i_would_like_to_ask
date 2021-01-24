<template>
  <div class="home">
    <p>
      Hola, soy <strong>Natanael Abad</strong>, estudiante de término de <strong>Ingeniera de Sistemas y Computacion</strong> 
      de la universidad Dominicana O{{charOne}}M. Como parte de mi proyecto monografico, me he propuesto realizar una 
      investigacion de caracter social, la que se basa en reconocer o identificar algunas de las razones que estan permitiendo 
      o que podrian permitir que las personas en nuestro pais caigan como victima de filtracion o robo de datos personales 
      (como contraseñas, datos bancarios o archivos privados) por parte de los archifamosos hackers.
    </p>

    <p>
      Actualmente, existe muy poca informacion de parte del estado sobre estadisticas o alguna otra informacion que pueda servir, por lo 
      que preferí crear mi propia fuente de referencia, pero para eso necesito que por favor, contestes algunas preguntas que he 
      creado para este proposito. <strong>No tendras que poner ningun dato personal, solo tus respuestas</strong>. 
      Si no tienes ningun desacuerdo y quieres contestarlas, presiona el link de abajo (donde dice continuar). Si no quieres hacerlo, solo 
      cierra la aplicacion (o página) y listo.
    </p>

    <p>
      Tambien quiero que tengas claro que <strong>lo unico que hace esta aplicacion es reunir los datos que pongas como 
      respuestas</strong>. Podras ver tus respuestas, tambien si quieres cambiar alguna respuesta, 
      cuando hayas contestado todo te dará la opción donde accedes a poder borrar alguna de ellas y luego podras volver a 
      contestarla. Tendras la opción de enviar tu cuestionario rellenado cuando quieras, luego que lo hayas enviado, ya no 
      podras volver a modificar nada.
    </p>

    <p>Si en algun momento notas que la aplicacion funciona de forma incorrecta o te parece que es dificil de usar, tienes la 
      posibilidad de <router-link to="/report">enviar un reporte</router-link> cuando quieras, explicando lo que pasa o alguna 
      idea que quisieras compartirme. 
    </p>

    <div id="nav" v-on:click="go()">
        <span class="r_link">Continuar</span>
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
      localStorage.setItem("iwouldliketoask", JSON.stringify({ stage: 0 }))
      this.$router.push({name: "Survey"})
    }
  },

  mounted () {
    let status = localStorage.getItem("iwouldliketoask")

    if(status != null) {
      status = JSON.parse(status)

      if(status.stage == 0) {
        this.$router.push({name: "Survey"})
      } else if(status.stage ==1) {
        this.$router.push({name: "Done"})
      }
    } else this.clienttoken()
  },
}
</script>

<style scoped>
.home a {
    text-decoration: none;
    color: #79c471;
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
