<template>
    <div>
        <Header/>
        <div class="quiz">
            <div class="quiz--item quiz--item--image-container">
                <img class="quiz--img" :src="image" alt="">
            </div>
            <div class="quiz--item quiz--result">
                <div class="quiz-result--container">
                    <div class="quiz-result--title">
                        {{title}}
                    </div>
                    <div class="quiz-result--text">
                        {{text}}
                    </div>
                    <div class="quiz-result--actions">
                        <div class="quiz-result--action"
                            v-on:click="$emit('again')">
                            <svg class="quiz-result--svg" width="30" height="27" viewBox="0 0 40 36" fill="none" xmlns="http://www.w3.org/2000/svg">
                                <path v-bind:d="this.path" fill="#7DBFFF"></path>
                            </svg>
                            Пройти еще раз
                        </div>
                        <div class="quiz-result--action">
                            <div class="social-icons">
                                <div class="icon"><img class="icon--img" src="../assets/twitter.svg" alt=""></div>
                                <div class="icon"><img class="icon--img" src="../assets/vk.svg" alt=""></div>
                                <div class="icon"><img class="icon--img" src="../assets/fb.svg" alt=""></div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="quiz-result--additional">
                    <div class="quiz-result--text">
                        Чтобы любая дорога была для вас безопасной,
                        следите за качеством резины и переобувайтесь вовремя.
                        С зимними шинами Cordiant ваша машина будет уверенно выезжать
                        из снежных заносов и стабильно вести себя на обледенелых трассах.
                        Прямо сейчас комплект зимних шин Cordiant можно купить со скидкой 15%!
                        Просто оформите заказ на <a href="">koleso.ru</a>, а потом позвоните по телефону 8-800-100-68-78,
                        назовите номер заказа и промокод <span class="promo">CORDIHACKER</span>.
                        <br><br>
                        Промокод действует до 30.10.2020.
                    </div>
                    <div class="quiz-result--text">
                        <div class="btn btn-action">
                            Купить шины со скидкой
                        </div>
                    </div>
                </div>
                <div class="footer-small">
                    <div class="footer-small--link">
                        <a href="">Лайфхакер</a>  | <a href="">Cordiant</a> © 2020
                    </div>
                    <div class="footer-small--link"><a href="">Команда проекта</a></div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Header from "./HeaderComponent";

    export default {
        name: "Result",
        components: { Header },
        props: {
            correct: {
                required: true
            },
            total: {
                required: true
            },
            results: {
                required: true
            }
        },
        data() {
            return {
                path: "M22.7161 0.716064C13.1883 0.716064 5.4403 8.4722 5.4403" +
                    " 18V18.0571L2.01944 12.9054C1.6847 12.3992 0.998893 12.2605" +
                    " 0.492703 12.5952C-0.0134861 12.9299 -0.15228 13.6157 0.182458" +
                    " 14.1219L5.14638 21.5923C5.326 21.8617 5.61175 22.0332 5.93016" +
                    " 22.074C5.97915 22.0822 6.01997 22.0822 6.06895 22.0822C6.33838" +
                    " 22.0822 6.59964 21.9842 6.80374 21.7964L13.7026 15.5833C14.1517" +
                    " 15.1751 14.1925 14.4812 13.7843 14.024C13.376 13.5749 12.6821" +
                    " 13.5341 12.2249 13.9423L7.64467 18.0816V18C7.64467 9.68052 14.4048" +
                    " 2.92044 22.7161 2.92044C31.0274 2.92044 37.7956 9.68052 37.7956" +
                    " 18C37.7956 26.3195 31.0355 33.0795 22.7242 33.0795C18.6992 33.0795" +
                    " 14.9109 31.512 12.0697 28.6626C11.637 28.2299 10.9431 28.2299 10.5104" +
                    " 28.6626C10.0776 29.0953 10.0776 29.7893 10.5104 30.222C13.7761 33.4878" +
                    " 18.1114 35.2839 22.7242 35.2839C32.2439 35.2839 40 27.5359 40 18C40" +
                    " 8.46403 32.2439 0.716064 22.7161 0.716064Z"
            }
        },
        computed: {
            level(){
                if (this.correct > 4) return 3;
                else if (this.correct > 2) return  2;
                else return  1;
            },
            image() {
                return require(`../assets/result${this.level}.jpg`)
            },
            title() {
                return this.results[this.level].title
            },
            text() {
                return this.results[this.level].text
            }
        }
    }
</script>

<style>
    .quiz--result {
        background: #004373;
        height: auto;
    }
    .quiz-result--container {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 100%;
        border-bottom: 2px solid white;
        padding: 80px 40px 20px 40px;
    }
    .quiz-result--title {
        width: 80%;
        font-weight: 600;
        font-size: 2rem;
        margin-top: 20px;
    }
    .quiz-result--text {
        width: 80%;
        margin-top: 25px;
    }
    .quiz-result--actions {
        display: flex;
        flex-direction: row;
        width: 80%;
        text-align: left;
    }
    .quiz-result--svg {
        vertical-align: middle;
        margin: 0 5px;
    }
    .quiz-result--action {
        color: #7DBFFF;
        margin: auto 0;
        width: 50%;
    }
    .quiz-result--action:hover {
        color: white;
    }
    .quiz-result--action:hover svg path {
        fill: white;
    }
    .quiz-result--additional {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 20px 40px;
    }
    .promo {
        background: #002B57;
        color: #96ede7;
        padding: 3px;
        border-radius: 3px;
    }
</style>