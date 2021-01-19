<template>
    <div id="control">

        <div id="back">
            <span v-on:click="goBack()">{{char_01}}</span>
        </div>

        <div id="view">
            <p id="question">
            {{currentQuestion}}
            </p>

            <div id="answers">
                <p>answers will be showed here</p>
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
                    question: "Question #1",
                    answers: ["Si", "No", "No sé"]
                },
                {
                    question: "Question #2",
                    answers: ["Si", "No", "No sé"]
                },
                {
                    question: "Question #3",
                    answers: ["Si", "No", "No sé"]
                }
                
            ], //array of objects

            pos: 0
        }
    },

    methods: {
        goNext () {
            let calcPos = this.pos + 1
            this.pos += 1

            if(calcPos > this.questionCollection.length - 1) {
                this.currentQuestion = this.questionCollection[0].question
                this.pos = 0
            } else {
                this.currentQuestion = this.questionCollection[calcPos].question
            }
        },

        goBack () {
            let calcPos = this.pos - 1
            this.pos -= 1

            if(calcPos == -1) {
                this.currentQuestion = this.questionCollection[this.questionCollection.length - 1].question
                this.pos = this.questionCollection.length - 1
            }
            else {
                this.currentQuestion = this.questionCollection[calcPos].question
            } 
        }
    }
}
</script>

<style scoped>

@media only screen and (min-width: 751px) {
    #control {
        display: flex;
        border: solid #888 2px;
        border-radius: 8px;
        margin-top: 15px;
        height: auto;
        padding: 15px;
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
    }

    #back:hover span {
        background: #79c471;
        border-radius: 50%
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
    }

    #answers {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
}

@media only screen and (max-width: 750px) {

    #control {
        display: flex;
        border: solid #888 2px;
        border-radius: 8px;
        margin: 15px 10px 0 10px;
        height: auto;
        padding: 10px;
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
        margin: 0px 10px;
        padding-bottom: 8px;
    }

    #back span {
        text-align: center;
        font-size: 45px;
        width: 60px;
        margin: 0px 10px;
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
    }

    #answers {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

}

</style>