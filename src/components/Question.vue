<template>
    <div>
        <div class="quiz">
            <div class="quiz--item quiz--item--image-container">
                <img class="quiz--img" :src="image" alt="">
                <transition name="fade">
                    <img class="quiz--img-top" src="../assets/question.png" alt=""
                        v-if="status==='asked'">
                </transition>
                <transition name="fade">
                    <img class="quiz--img-top" src="../assets/right.png" alt=""
                        v-if="status==='right'">
                </transition>
                <transition name="fade">
                    <img class="quiz--img-top" src="../assets/wrong.png" alt=""
                         v-if="status==='wrong'">
                </transition>
                <img class="quiz--img-bottom" src="../assets/wheel.png" alt="">
            </div>
            <div class="quiz--item quiz--text">
                <div class="quiz--text--wrapper">
                    <div class="quiz--counter">{{ this.index + 1 + ' / ' + this.total}}</div>
                    <div v-if="status==='asked'">
                        <div class="quiz--container">
                            <div class="quiz--title"
                                 v-html="this.question.text">
                            </div>
                            <div class="btn btn-option"
                                 v-for="option in this.question.answers"
                                 v-on:click="handleAnswer(option)"
                                 v-html="option.text">
                            </div>
                        </div>
                    </div>
                    <div v-if="status!=='asked'">
                        <div class="quiz--container">
                            <div class="quiz--feedback" v-html="this.feedback"></div>
                            <div class="quiz--additional" v-html="this.question.additional"></div>
                            <div class="btn btn-action"
                                 v-on:click="nextQuestion">
                                Далее
                            </div>
                        </div>
                    </div>
                </div>
                <div class="footer-small footer-absolute">
                    <div class="footer-small--link">
                        <a href="">Лайфхакер</a>  | <a href="">Cordiant</a> © 2020
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Question",
        props: {
            question: {
                required: true
            },
            index: {
                required: true
            },
            total: {
                required: true
            }
        },
        data () {
            return {
                status: 'asked',
                feedback: '',
            }
        },
        computed: {
            image() {
                return require(`../assets/${this.index + 1}.jpeg`)
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
    .btn-option {
        background: rgba(255, 255, 255, 0.2);
    }
    .btn-option:hover, .btn-option:hover strong {
        background: #7DBFFF;
        color: #004373;
    }
    .btn-option:active {
        color: #004373;
        background: white;
    }
    .quiz--text--wrapper {
        min-height: 50vh;
    }
    .fade-leave-active {
        transition: opacity .4s;
    }
    .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
        opacity: 0;
    }
</style>