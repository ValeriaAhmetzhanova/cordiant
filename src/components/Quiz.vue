<template>
    <div>
        <div v-if="status==='start'">
            <StartScreen v-on:startQuiz="next"/>
        </div>
        <div v-if="status==='quiz'">
            <Question
                    v-bind:question="this.questions[questionIndex]"
                    v-bind:index="this.questionIndex"
                    v-bind:total="this.questions.length"
                    v-bind:additional="this.questions[questionIndex].additional"
                    v-on:answer="handleAnswer"
                    v-on:next="next"
            />
        </div>
        <div v-if="status==='result'">
            {{ this.correct }} / {{ this.questions.length }}
        </div>
    </div>
</template>

<script>
    import StartScreen from './StartScreen'
    import Question from "./Question";

    export default {
        data() {
            return {
                questionIndex: 0,
                status: "start",
                correct: 0
            }
        },
        props: {
            questions: {
                required: true
            }
        },
        methods: {
            next() {
                if (this.status === 'start') this.status = 'quiz';
                else if (this.questionIndex + 1 < this.questions.length) this.questionIndex++;
                else this.status = 'result';
            },
            handleAnswer(option) {
                if (option.correct) this.correct++;
            },
        },
        components: {
            StartScreen,
            Question
        }
    }
</script>

<style>
    * {
        font-family: "Open Sans", sans-serif;
        color: white;
        box-sizing: border-box;
    }
    body, div {
        margin: 0;
    }
    a {
        color: #7DBFFF;
    }
    .btn {
        padding: 16px 70px;
        border-radius: 3px;
        width: auto;
        margin: 15px 0;
        font-size: 1.2rem;
    }
    .btn-action {
        background: #7DBFFF;
        color: #004373;
    }
    .btn-action:hover {
        background: white;
    }
    .footer {
        position: fixed;
        padding: 30px;
        bottom: 0;
    }
    .footer-small {
        position: fixed;
        padding: 20px;
        bottom: 0;
        width: 35%;
        text-align: right;
    }
</style>