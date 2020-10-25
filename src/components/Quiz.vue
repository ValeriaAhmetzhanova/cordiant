<template>
    <div id="main">
        <Header/>
        <div v-if="status==='start'">
            <StartScreen v-on:startQuiz="next"/>
        </div>
        <div v-if="status==='quiz'">
            <Question
                    v-bind:question="this.questions[questionIndex]"
                    v-bind:index="this.questionIndex"
                    v-bind:total="this.questions.length"
                    v-on:answer="handleAnswer"
                    v-on:next="next"
            />
        </div>
        <div v-if="status==='result'">
            <Result
                    v-bind:correct="this.correct"
                    v-bind:total="this.questions.length"
                    v-bind:results="results"
                    v-on:again="reset"
            />
        </div>
    </div>
</template>

<script>
    import StartScreen from './StartScreen'
    import Question from "./Question";
    import Result from "./Result";
    import Header from "./HeaderComponent";

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
            },
            results: {
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
            reset(){
               this.questionIndex = 0;
               this.status = "quiz";
               this.correct = 0;
            }
        },
        components: {
            StartScreen,
            Question,
            Result,
            Header
        }
    }
</script>

<style>
    * {
        font-family: "PT Sans", sans-serif;
        color: white;
        box-sizing: border-box;
        line-height: 1.5;
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
    }
    .btn-action {
        background: #7DBFFF;
        width: fit-content;
        color: #004373;
        text-align: center;
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
        display: flex;
        flex-direction: row-reverse;
        padding: 20px;
        bottom: 0;
        text-align: right;
    }
    .footer-small--link {
        margin: 0 15px;
    }
    .footer-relative {
        position: relative;
        width: 90%;
    }
    .quiz {
        display: flex;
        width: 100%;
    }
    .quiz--item {
        justify-content: center;
        width: 50%;
        background-repeat: no-repeat;
        overflow-x: hidden;
    }
    .quiz--item--image-container {
        display: flex;
    }
    .quiz--img {
        position: relative;
        height: 100vh;
        flex: none;
    }
    .quiz--img-top{
        position: absolute;
        top: 0;
        width: 40%;
    }
    .quiz--img-bottom {
        position: absolute;
        bottom: 0;
        left: 0;
        width: 100%;
        height: auto;
    }
    .quiz--text {
        background: #004373;
        height: auto;
        padding: 100px 80px;
    }
    .quiz--title {
        text-align: center;
        margin: 20px;
        font-size: 2rem;
        font-weight: 600;
    }
    .quiz--feedback {
        font-weight: 600;
        margin: 20px 0;
    }
    .quiz--additional {
        margin: 30px 0;
    }
    @media only screen and (max-width: 991px) {
        .btn-action {
            width: 100%;
        }
        .quiz {
            flex-direction: column;
        }
        .quiz--item {
            width: 100%;
        }
        .quiz--img {
            width: 100vw;
            height: 62vw;
        }
        .quiz--img-bottom {
            display: none;
        }
        .quiz--text {
            padding: 20px;
            border-top: 2px solid white;
            min-height: 70vh;
        }
    }
    @media only screen and (min-width: 992px) {
        .quiz--item--image-container {
            position: sticky;
            align-self: flex-start;
            top: 0;
        }
        .quiz--img-top {
            left: 50%;
        }
        .quiz--container {
            width: 90%;
            padding: 30px 20px;
        }
        .footer-absolute {
            position: absolute;
            width: 40%;
        }
        .footer-small--link {
            display: inline-block;
            width: 50%;
        }
        .btn {
            font-size: 1.2rem;
        }
    }
</style>