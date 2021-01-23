<template>
    <div class="question-box-container">
        <b-jumbotron>

            <template #lead>
            {{ currentQuestion.question }}
            </template>

            <hr class="my-4">

            <b-list-group>
                <b-list-group-item 
                v-for="(answer, index) in answers" :key="index"
                @click.prevent="selectAnswer(index)" 
                :class="[selectedIndex === index ? 'selectedAnswer' : '']"
                >
                    {{ answer }}
                </b-list-group-item>
            </b-list-group>

            <b-button 
                variant="primary"
                @click="submitAnswer"
            >
                Submit
            </b-button>
            <b-button @click="next" variant="success" href="#">
                Next
            </b-button>
        </b-jumbotron>
    </div>
</template>

<script>
import _ from "lodash"
export default {
    props: {
        currentQuestion: Object, 
        next: Function,
        increment: Function
    },
    data() {
        return {
            selectedIndex: null,
            correctIndex: null,
            shuffledAnswers: [],
        }
    }, 
    computed: {
        answers() {
            let answers = [...this.currentQuestion.incorrect_answers]
            answers.push(this.currentQuestion.correct_answer)
            return answers
        }
    }, 
    watch: {
        currentQuestion: {
            immediate: true,
            handler() {
                this.selectedIndex = null;
                this.shuffleAnswers()
            }
        }
    },
    methods: {
        selectAnswer(index) {
            this.selectedIndex = index
        },
        shuffleAnswers() {
            let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
            this.shuffledAnswers = _.shuffle(answers)
        },
        submitAnswer() {
            let isCorrect = false

            if (this.selectedIndex === this.correctIndex) {
                isCorrect = true
            }

            this.increment(isCorrect)
        }
    }
}
</script>

<style scoped>
    .list-group {
        margin-bottom: 15px;
    }

    .list-group-item:hover {
        background: #EEE;
        cursor: pointer;
    }

    .btn {
        margin: 0 5px;
    }

    .selectedAnswer {
        background-color: lightblue;
    }

    .correctAnswer {
        background-color: lightgreen;
    }

    .incorrectAnswer {
        background-color: lightcoral;
    }
</style>