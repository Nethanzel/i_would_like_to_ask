<template>
    <div id="control">

        <div id="back">
            <span v-on:click="goBack()">{{char_01}}</span>
        </div>

        <div id="view">
            <p id="question">
                {{currentQuestion}}
            </p>

            <img src="" id="viewImg">

            <div id="answers">
            </div>
        </div>

        <div id="next">
            <span v-on:click="goNext()">></span>
        </div>

    </div>
</template>

<script>
export default {
    name: "Questions",
    data() {
        return {
            char_01: "<",
            currentQuestion: "",
            questionCollection: [
                {
                    question: "Se verá bien en los navegadores más modernos, aunque en versiones anteriores era una propiedad no estándar con prefijo, así que si queremos que funcione en versiones anteriores de firefox, chrome, opera o safari deberíamos incluir los códigos con prefijos, aunque de aquí a unos años con el código superior sería suficiente, actualmente si es recomendable incluir:",
                    answers: ["Si", "No", "No sé"],
                    type: "multi",
                    img: true,
                    uri: "https://dia8publicidad.com/wp-content/uploads/2020/05/Imagen-redes-01.jpg"
                },
                {
                    question: "Question #2",
                    answers: ["Si", "No", "No sé"],
                    type: "text",
                    img: true,
                    uri: "https://www.eluniversal.com.mx/sites/default/files/2020/03/19/como_extraer_un_texto_de_una_imagen.jpg"
                },
                {
                    question: "Question #3",
                    answers: ["Si", "No", "No sé"],
                    type: "pick",
                    img: false
                }
                
            ], //array of objects

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
        },

        renderAnswer (questionAnswers, type) {

            this.type = type
            let answersView = document.getElementById("answers")
            if(type == "pick") {
                answersView.style.paddingLeft = "20px"
                answersView.innerHTML = ""
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
                for(let i = 0; i < questionAnswers.length; i++) {
                    let option = `
                        <input type="checkbox" name="option" id="option${i}" value="${questionAnswers[i]}" style="margin: 7px 5px;"> 
                        <label for="option${i}">${questionAnswers[i]}</label> <br>
                    `
                    answersView.innerHTML += option
                }
                answersView.innerHTML += '<p style="margin: 7px 5px;">(Puedes elegir más de una)</p>'
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
                this.storageResutls(questionResult) //Value to save as an answered question
            }
        },

        storageResutls(value) {
            let storage = localStorage.getItem("questionStorage")

            if(storage != null) {
                storage = JSON.parse(storage)
                storage.questions.push(value)
                localStorage.setItem("questionStorage", JSON.stringify(storage))
            } else {
                localStorage.setItem("questionStorage", JSON.stringify({questions: []}))
                this.storageResutls(value)
            }
        }
    },

    mounted () {
        let Pos = 0
        this.currentQuestion = this.questionCollection[Pos].question
        this.renderAnswer(this.questionCollection[Pos].answers, this.questionCollection[Pos].type)
        this.rederImg(this.questionCollection[Pos])

        let image = document.getElementById("viewImg")

        image.addEventListener("click", (e) => {
            let uri = e.target.getAttribute("src")
            this.$emit("view", uri)
        })
    }
}
</script>

<style scoped>

#viewImg {
    max-width: 25vw;
    margin-bottom: 15px; 
    display: none;
}

@media only screen and (min-width: 751px) {
    #control {
        display: flex;
        border: solid #888 2px;
        border-radius: 8px;
        margin: 5px 10px 5px 10px;
        height: auto;
        max-height: 650px;
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
        /*display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;*/
        width: 100%;
    }
}

@media only screen and (max-width: 750px) {

    #control {
        display: flex;
        border: solid #888 2px;
        border-radius: 8px;
        margin: 5px 10px 0 10px;
        height: auto;
        padding: 0 5px;
        min-width: 300px;
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

}



</style>