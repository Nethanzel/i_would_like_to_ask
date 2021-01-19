<template>
    <div class="report">
      <h1>¡Ayudame a alcanzar la meta diciendome si la aplicacion tiene fallos!</h1>
      <p>Puedes usar una de las dos opciones a continuacion: </p>

      <h3>Envia un reporte</h3>
      <form action="">
          <h2>Reportar fallos</h2>
          <label for="donde">¿Donde fallo la aplicacion? (poner el link)</label> <input type="url" id="donde"> <br>
          <label for="desc">Agrega una pequeña descripcion: </label> <input type="text" aria-multiline="true" id="desc"> <br>
          <label for="capt">Agrega alguna captura: </label> <input type="file" accept="image/*" multiple id="capt">
      </form>

      <h3>Enviame un mensaje</h3>
    </div>
</template>

<style scoped>
@media only screen and (max-width: 750px) {
  .report {
    height: auto;
    cursor: default;
    padding-top: 10vh;
    margin: 0 10px 15px 10px;
    min-width: 350px;
  }

  h1 {
    text-align: center;
    margin-bottom: 20px;
  }

  p {
    margin-bottom: 15px;
    font-size: 17px;
    margin: 0 10px 15px 10px;
  }

  form {
    margin: 10px 10px;
    padding: 10px 5px 15px 5px;
    border-radius: 5px;
    background: #858484;
  }

  form > *{
    margin: 5px 5px 15px 5px;
  }

  h2 {
    text-align: center;
    margin-bottom: 15px;
  }

  input[type=text]:focus {
    outline: none;
  }

  input[type=url]:focus {
    outline: none;
  }

}

@media only screen and (min-width: 751px) {
  .report {
    height: auto;
    cursor: default;
    margin: 0 10px 15px 10px;
    padding-top: 8vh;
    display: flex;
    flex-direction: column;
  }

  h1 {
    text-align: center;
    margin-bottom: 20px;
  }

  p {
    margin-bottom: 15px;
    font-size: 19px;
    margin: 0 10px 15px 10px;
  }

   form {
    max-width: 600px;
    align-self: center;
    margin: 10px 10px;
    padding: 15px 5px 15px 5px;
    border-radius: 5px;
    background: #858484;
  }

  form > *{
    margin: 5px 5px 15px 5px;
  }

  h2 {
    text-align: center;
    margin-bottom: 15px;
  }

  input[type=text]:focus {
    outline: none;
  }

  input[type=url]:focus {
    outline: none;
  }


}
</style>