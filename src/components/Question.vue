<template>
    <div>
        <Header/>
        <div class="quiz">
            <div class="quiz--item quiz--item--image-container">
                <img class="quiz--img" :src="image" alt="">
                <img class="quiz--img-top" src="../assets/question.png" alt=""
                    v-if="status==='asked'">
                <img class="quiz--img-top" src="../assets/right.png" alt=""
                    v-if="status==='right'">
                <img class="quiz--img-top" src="../assets/wrong.png" alt=""
                     v-if="status==='wrong'">
                <img class="quiz--img-bottom" src="../assets/wheel.png" alt="">
            </div>
            <div class="quiz--item quiz--text">
                <div>
                    <div class="quiz--counter">{{ this.index + 1 + ' / ' + this.total}}</div>
                    <div v-if="status==='asked'">
                        <div class="quiz--container">
                            <div class="quiz--title">
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
                        <div class="quiz--container">
                            <div class="quiz--feedback">{{ this.feedback }}</div>
                            <div class="quiz--additional">{{ additional }}</div>
                            <div class="btn btn-action"
                                 v-on:click="nextQuestion">
                                Далее
                            </div>
                        </div>
                    </div>
                </div>
                <div class="footer-small">
                    <div class="footer-small--link">
                        <a href="">Лайфхакер</a>  | <a href="">Cordiant</a> © 2020
                    </div>
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