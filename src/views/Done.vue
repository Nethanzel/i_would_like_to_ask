<template>
    <div id="done">
        <h1>¡Has participado! Gracias por tu ayuda.</h1>
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

@media only screen and (max-width: 750px) {

    #done {
        height: auto;
        cursor: default;
        padding-top: 9.5vh;
    }

    h1 {
        text-align: center;
    }
}

@media only screen and (min-width: 751px) {
    #done {
        height: auto;
        cursor: default;
        padding-top: 7.5vh;
    }

    h1 {
        text-align: center;
    }
}

</style>