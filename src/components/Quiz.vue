<template>
    <div>
        <div id="start" v-if="status==='start'">
            <StartScreen v-on:startQuiz="next"/>
        </div>
        <div v-if="status==='quiz'">
            {{this.questions[questionIndex].text}}
            <div
                    v-for="option in this.questions[questionIndex].answers"
                    v-on:click="handleAnswer(option)">
                {{ option.text }}
            </div>
        </div>
        <div v-if="status==='result'">
            {{ this.correct }} / {{ this.questions.length }}
        </div>
    </div>
</template>

<script>
    import StartScreen from './StartScreen'

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
                this.next();
            }
        },
        components: {
            StartScreen
        }
    }
</script>

<style>
    * {
        font-family: "Open Sans", sans-serif;
    }
    body, div {
        margin: 0;
    }
    .btn {
        padding: 16px 70px;
        background: #7DBFFF;
        border-radius: 3px;
        width: fit-content;
        color: #004373;
        margin: 15px 0;
        font-size: 1.2rem;
    }
</style>