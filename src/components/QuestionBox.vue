<template>
    <div class="question-box-container">
        <b-jumbotron>

            <template #lead>
            {{ currentQuestion.question }}
            </template>

            <hr class="my-4">

            <p>
            Answers go here
            </p>

            <b-button variant="primary" href="#">Submit</b-button>
            <b-button @click="next" variant="success" href="#">
                Next
            </b-button>
        </b-jumbotron>
    </div>
</template>

<script>
export default {
    props: {
        currentQuestion: Object, 
        next: Function
    },
    mounted() {
        console.log(this.currentQuestion)
    }
}
</script>