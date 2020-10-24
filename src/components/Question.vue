<template>
    <div id="quiz">
        <Header/>
        <div class="question">
            <div class="question--item question--item--image-container">
                <img class="question--img" :src="image" alt="">
                <img class="question--img-top" src="../assets/question.png" alt=""
                    v-if="status==='asked'">
                <img class="question--img-top" src="../assets/right.png" alt=""
                    v-if="status==='right'">
                <img class="question--img-top" src="../assets/wrong.png" alt=""
                     v-if="status==='wrong'">
                <img class="question--img-bottom" src="../assets/wheel.png" alt="">
            </div>
            <div class="question--item question--text">
                <div>
                    <div class="question--counter">{{ this.index + 1 + ' / ' + this.total}}</div>
                    <div v-if="status==='asked'">
                        <div class="question--conainer">
                            <div class="question--title">
                                {{ this.question.text }}
                            </div>
                            <div class="btn btn-option"
                                 v-for="option in this.question.answers"
                                 v-on:click="handleAnswer(option)">
                                {{ option.text }}
                            </div>
                        </div>
                    </div>
                    <div v-if="status!=='asked'">
                        <div class="question--container">
                            <div class="question--feedback">{{ this.feedback }}</div>
                            <div class="question--additional">{{ additional }}</div>
                            <div class="btn btn-action"
                                 v-on:click="nextQuestion">
                                Далее
                            </div>
                        </div>
                    </div>
                </div>
                <div class="footer-small">
                    <a href="">Лайфхакер</a>  | <a href="">Cordiant</a> © 2020
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Header from "./HeaderComponent";

    export default {
        name: "Question",
        components: { Header },
        props: {
            question: {
                required: true
            },
            index: {
                required: true
            },
            total: {
                required: true
            },
            additional: {}
        },
        data () {
            return {
                status: 'asked',
                feedback: '',
            }
        },
        computed: {
            image() {
                return require(`../assets/${this.index + 1}.png`)
            }
        },
        methods: {
            handleAnswer(option) {
                if (option.correct) this.status = 'right';
                else this.status = 'wrong';
                this.$emit('answer', option);
                this.feedback = option.feedback;
            },
            nextQuestion() {
                this.reset();
                this.$emit('next');
            },
            reset() {
                this.status = 'asked';
                this.feedback = '';
            }
        }
    }
</script>

<style>
    .question {
        display: flex;
        width: 100%;
    }
    .question--item {
        justify-content: center;
        height: 100vh;
        width: 50%;
        background-repeat: no-repeat;
        overflow: hidden;
    }
    .question--item--image-container {
        display: flex;
    }
    .question--img {
        position: relative;
        height: 100vh;
        flex: none;
    }
    .question--img-top{
        position: absolute;
        top: 0;
        left: 25%;
        width: 20%;
    }
    .question--img-bottom {
        position: absolute;
        bottom: 0;
        left: 0;
        width: inherit;
        height: auto;
    }
    .question--text {
        background: #004373;
        height: auto;
        padding: 100px 80px;
    }
    .question--container {
        width: 90%;
        padding: 30px 20px;
    }
    .question--title {
        text-align: center;
        margin: 20px;
        font-size: 2rem;
        font-weight: 600;
    }
    .question--feedback {
        font-weight: 600;
        margin: 20px 0;
    }
    .question--additional {
        margin: 30px 0;
    }
    .btn-option {
        background: rgba(255, 255, 255, 0.2);
    }
    .btn-option:hover {
        background: #7DBFFF;
        color: #004373;
    }
    .btn-option:active {
        background: white;
    }
</style>