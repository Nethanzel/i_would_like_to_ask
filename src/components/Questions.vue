<template>
    <div id="control">

        <div id="back" v-on:click="goBack()">
            <span>{{char_01}}</span>
        </div>

        <div id="view">
            <p id="question">
                {{currentQuestion}}
            </p>

            <img src="" id="viewImg">

            <div id="answers">
            </div>
        </div>

        <div id="next" v-on:click="goNext()">
            <span>></span>
        </div>

    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: "Questions",
    data() {
        return {
            char_01: "<",
            currentQuestion: "",
            questionCollection: undefined, //array of objects
            pos: 0,
            type: ""
        }
    },

    methods: {
        goNext () {
            this.saveAnswer()
            let calcPos = this.pos + 1
            this.pos += 1

            if(calcPos > this.questionCollection.length - 1) {
                this.currentQuestion = this.questionCollection[0].question
                this.pos = 0
                this.renderAnswer( this.questionCollection[this.pos].answers,  this.questionCollection[this.pos].type)
                this.rederImg(this.questionCollection[this.pos])
            } else {
                this.currentQuestion = this.questionCollection[calcPos].question
                this.renderAnswer( this.questionCollection[calcPos].answers,  this.questionCollection[calcPos].type)
                this.rederImg(this.questionCollection[calcPos])
            }
            this.determineEnd()
        },

        goBack () {
            let calcPos = this.pos - 1
            this.pos -= 1

            if(calcPos == -1) {
                this.currentQuestion = this.questionCollection[this.questionCollection.length - 1].question
                this.pos = this.questionCollection.length - 1
                this.renderAnswer( this.questionCollection[this.pos].answers,  this.questionCollection[this.pos].type)
                this.rederImg(this.questionCollection[this.pos])
            }
            else {
                this.currentQuestion = this.questionCollection[calcPos].question
                this.renderAnswer( this.questionCollection[calcPos].answers,  this.questionCollection[calcPos].type)
                this.rederImg(this.questionCollection[calcPos])
            }
            this.determineEnd()
        },

        renderAnswer (questionAnswers, type) {

            this.type = type
            let answersView = document.getElementById("answers")
            if(type == "pick") {
                answersView.style.paddingLeft = "20px"
                answersView.innerHTML = ""
                answersView.style.display = "block"

                for(let i = 0; i < questionAnswers.length; i++) {
                    let option = `
                        <input type="radio" name="option" id="option${i}" value="${questionAnswers[i]}" style="margin: 7px 5px;"> 
                        <label for="option${i}">${questionAnswers[i]}</label> <br>
                    `
                    answersView.innerHTML += option
                }
            } else if(type == "multi") {
                answersView.style.paddingLeft = "20px"
                answersView.innerHTML = ""
                answersView.style.display = "block"

                for(let i = 0; i < questionAnswers.length; i++) {
                    let option = `
                        <input type="checkbox" name="option" id="option${i}" value="${questionAnswers[i]}" style="margin: 7px 5px;"> 
                        <label for="option${i}">${questionAnswers[i]}</label> <br>
                    `
                    answersView.innerHTML += option
                }
                answersView.innerHTML += '<p style="margin: 7px 5px;">(Puedes elegir más de una)</p>'
            } else if(type == "text"){
                answersView.style.paddingLeft = "0px"
                answersView.innerHTML = ""
                answersView.style.display = "flex"

                let option = `
                        <textarea id="textarea" name="option" placeholder="Escriba su respuesta."></textarea>
                    `
                    answersView.innerHTML += option

            } else if(type == "select"){
                answersView.style.paddingLeft = "20px"
                answersView.innerHTML = ""
                answersView.style.display = "flex"

                let option = `
                        <select id="select" name="option" placeholder="Escriba su respuesta.">
                        <option value="" disabled selected>Seleccione...</option>
                    `
                for(let i = 0; i < questionAnswers.length; i++) {
                    option += `
                    <option value="${questionAnswers[i]}">${questionAnswers[i]}</option>
                    `
                }
                    answersView.innerHTML += option + "</select>"

            } else {
                answersView.style.paddingLeft = "0px"
                answersView.innerHTML = ""
            }
        },

        rederImg(obj) {

            let imgview = document.getElementById("viewImg")
            if(obj.img) {
                imgview.src = obj.uri
                imgview.style.display = "flex"
            } else {
                imgview.src = ""
                imgview.style.display = "none"
            }
        },

        saveAnswer() {

            if(this.type == "multi" || this.type == "pick") {

                let question  = ""
                let answer = []
                let options = document.getElementsByName("option")

                question = this.currentQuestion //here you catch the question
                for(let i = 0; i < options.length; i++) {
                    if(options[i].checked) {
                        answer.push(options[i].value) //here you catch the answer
                    }
                }
                let questionResult = {
                    question,
                    answer,
                    pos: this.pos
                }

                if(answer.length == 0) {
                    return null
                }

                this.storageResutls(questionResult) //Value to save as an answered question

            } else if(this.type == "text") {

                let question  = ""
                let text = document.getElementById("textarea")
                let answer = [text.value]

                question = this.currentQuestion //here you catch the question

                let questionResult = {
                    question,
                    answer,
                    pos: this.pos
                }

                if(answer[0].length == 0) {
                    return null
                }

                this.storageResutls(questionResult) //Value to save as an answered question
            } else if(this.type == "select") {

                let question  = ""
                let slect = document.getElementById("select")
                let answer = [slect.value]

                question = this.currentQuestion //here you catch the question

                let questionResult = {
                    question,
                    answer,
                    pos: this.pos
                }

                if(answer[0] == "") {
                    return null
                }

                this.storageResutls(questionResult) //Value to save as an answered question
            }
        },

        storageResutls(value) {
            let exists = this.validateAnswers(value)
            let storage = localStorage.getItem("questionStorage")
             if(storage != null) {
                if(!exists) {
                    storage = JSON.parse(storage)
                    storage.questions.push(value)
                    localStorage.setItem("questionStorage", JSON.stringify(storage))
                }
            } else {
                localStorage.setItem("questionStorage", JSON.stringify({questions: []}))
                this.storageResutls(value)
            }
        },

        loadQuestions() {
            let token = this.clienttoken()

            axios.get("/api/questions", {headers: {"token": token}})

            .then(res => {
                this.questionCollection = res.data.data
                this.$emit("count", this.questionCollection.length)
                this.dataLoaded()
            })
            .catch((err) => {
                let e = String(err).toLowerCase()
                if(e.includes("network error")) {
                    this.messageBox("Servidor fuera de alcance.", 2)
                } else if (e.includes("code 401")) {
                    this.messageBox("Autenticación requerida o invalida.", 0)
                } else if (e.includes("code 404")) {
                    this.messageBox("Solictud invalida.", 0)
                } else if(e.includes("code 500")) {
                    this.messageBox("Estamos teniendo algunos problemas con el servidor.", 2)
                } else {
                 this.messageBox("Error desconocido.", 0)
                }
            })
        },

        validateAnswers(newAnser) {
            let storage = localStorage.getItem("questionStorage")
            if(storage != null) {
                storage = JSON.parse(storage)
                let answers = storage.questions

                for(let i = 0; i < answers.length; i++) {
                    if(newAnser.question == answers[i].question){

                        if(confirm("Ya habias respondido esta, ¿quieres guardar la nueva respuesta?")) {
                            let vStorage = storage
                            vStorage.questions.splice(i, 1)
                            localStorage.setItem("questionStorage", JSON.stringify(vStorage))
                            return false
                        } else return true
                    }
                }
                return false
            }
        },

        determineEnd() {
            let storage = localStorage.getItem("questionStorage")
            if(storage != null) {
                storage = JSON.parse(storage)
                let answers = storage.questions

                if(answers.length == this.questionCollection.length) {
                    this.$emit("finished", true)
                } else {
                    this.$emit("finished", false)
                }
            }
        },
        dataLoaded() {
            this.currentQuestion = this.questionCollection[0].question
            this.renderAnswer(this.questionCollection[0].answers, this.questionCollection[0].type)
            this.rederImg(this.questionCollection[0])

            let image = document.getElementById("viewImg")
            image.addEventListener("click", (e) => {
                let uri = e.target.getAttribute("src")
                this.$emit("view", uri)
            })
            this.determineEnd()
            this.$emit("count", this.questionCollection.length)
        }
    },

    mounted () {
        document.getElementById("svSpin").style.display = "block"
        this.loadQuestions()
    }
}
</script>

<style>

#viewImg {
    max-width: 25vw;
    margin-bottom: 15px; 
    display: none;
}

#textarea {
    padding: 5px;
    color: #000;
    resize: none;
    outline: none;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    margin-left: auto;
    margin-right: auto;
}

@media only screen and (min-width: 751px) {
    #control {
        display: flex;
        border: solid #888 2px;
        border-radius: 8px;
        margin: 5px 10px 5px 10px;
        height: auto;
        max-height: 650px;
        background: #c9c9c959;
        box-shadow: 5px 5px 5px #0000008d;
        transition: .5s,;
    }

    #next {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    #back {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    #next span {
        text-align: center;
        font-size: 52px;
        width: 70px;
        margin: 10px 10px;
        padding-bottom: 8px;
    }

    #back span {
        text-align: center;
        font-size: 52px;
        width: 70px;
        margin: 10px 10px;
        padding-bottom: 8px;
    }

    #next:hover span {
        background: #79c471;
        border-radius: 50%;
        transition: all .5s;
    }

    #back:hover span {
        background: #79c471;
        border-radius: 50%;
        transition: all .5s;
    }

    #view {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 15px 10px;
        min-width: 450px;
    }

    #question {
        display: block;
        padding: 15px 0;
        font-size: 19px;
        font-weight: bold;
        text-align: center;
    }

    #answers {
        width: 100%;
    }

    #textarea {
        font-size: 17px;
        font-family: monospace;
        height: 100px;
        width: 90%;
    }

    #select {
        font-size: 17px;;
    }
}

@media only screen and (max-width: 750px) {

    #control {
        display: flex;
        border: solid #bbb 2px;
        background: #c9c9c959;
        border-radius: 8px;
        margin: 5px 5px 0 5px;
        height: auto;
        padding: 0 5px;
        min-width: 300px;
        transition: .5s;
        box-shadow: 3px 5px 5px #0000008d;
    }

    #next {
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }

    #back {
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }

    #next span {
        text-align: center;
        font-size: 45px;
        width: 60px;
        padding-bottom: 8px;
    }

    #back span {
        text-align: center;
        font-size: 45px;
        width: 60px;
        padding-bottom: 8px;
    }

    #next:active span {
        background: #79c471;
        border-radius: 50%;
    }

    #back:active span {
        background: #79c471;
        border-radius: 50%
    }

    #view {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 10px 5px;
        width: 100%;
        min-width: 55vw;
    }
 
    #question {
        display: block;
        padding: 15px 0;
        font-size: 17px;
        font-weight: bold;
        text-align: center
    }

    #answers {
        /*display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;*/
        width: 100%;
    }

    #textarea {
        font-size: 17px;
        height: 75px;
        width: 100%;
    }

    #select {
        font-size: 17px;
        width: 100%;
    }

}
</style>