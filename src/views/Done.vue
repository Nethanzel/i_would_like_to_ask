<template>
    <div id="done">
        <h1>¡Ya has colaborado! Gracias por tu ayuda.</h1>
        <p>Si quieres seguir aportando, por favor pidele a tus amgios que tambien participen.</p>
        <p>Si quieres ver el progreso de la recoleccion de datos, <router-link to="/overview" class="link">aqui
        </router-link> podras ver un resumen.</p>
    </div>
</template>

<script>
export default {
    name: "done",
    title: "I would like to ask...",
    beforeCreate() {
        let status = localStorage.getItem("iwouldliketoask")
        if(status == null) {
            this.$router.push("/")
        } else {
            if (status.stage == 0) {
                this.$router.push("/survey")
            }
        }

        }
}
</script>


<style scoped>

a {
    text-decoration: none;
    color: #79c471;
}

@media only screen and (max-width: 750px) {

    #done {
        height: auto;
        cursor: default;
        padding-top: 9.5vh;
    }

    h1 {
        text-align: center;
    }

    p{
        text-align: center;
        font-size: 17px;
    }
}

@media only screen and (min-width: 751px) {
    #done {
        height: auto;
        cursor: default;
        padding-top: 9.5vh;
    }

    h1 {
        text-align: center;
    }

    p{
        text-align: center;
        font-size: 19px;
    }
}

</style>