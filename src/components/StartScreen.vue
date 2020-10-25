<template> 
    <div>
        <div id="start">
            <div class="start-info">
                <div class="start-info--title">
                    Узнаете ли вы Россию
                    <br>
                    <strong>ПО ДОРОГАМ?</strong>
                </div>
                <div class="start-info--text">
                    <div class="start-info--container">
                        Мы составили этот тест вместе с производителем шин <a href="">Cordiant</a>,
                        чтобы вы проверили, сможете ли отличить российские дороги
                        от остальных. Активируйте внутреннего Шерлока — и вперёд!
                        Пройдёте тест до конца — получите <strong>скидку 15%</strong> на зимнюю резину.
                        <div class="btn btn-action"
                             v-on:click="$emit('startQuiz')">
                            Пройти тест!
                        </div>
                    </div>
                </div>
                <div class="footer-mobile">
                    <div class="social-icons">
                        <div class="icon"><img class="icon--img" src="../assets/twitter.svg" alt=""></div>
                        <div class="icon"><img class="icon--img" src="../assets/vk.svg" alt=""></div>
                        <div class="icon"><img class="icon--img" src="../assets/fb.svg" alt=""></div>
                    </div>
                </div>
            </div>
        </div>
        <div class="footer">
            <div class="social-icons social-icons-left">
                <div class="icon"><img class="icon--img" src="../assets/twitter.svg" alt=""></div>
                <div class="icon"><img class="icon--img" src="../assets/vk.svg" alt=""></div>
                <div class="icon"><img class="icon--img" src="../assets/fb.svg" alt=""></div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "StartScreen",
    };
</script>

<style>
    #start {
        background: url("../assets/start-background.png") no-repeat center center fixed;
        -webkit-background-size: cover;
        -moz-background-size: cover;
        -o-background-size: cover;
        background-size: cover;
        box-shadow: inset 0 40px 50px -20px black;
        height: 100vh;
    }
    .start-info {
        width: 50%;
        background: #004373;
        text-align: center;
        border: 2px solid white;
        border-right: none;
        margin-left: auto;
        margin-right: 0;
        position: relative;
        top: 15%;
    }
    .start-info--title {
        padding: 30px;
        border-bottom: 2px solid white;
        margin-bottom: 8px;
        font-size: 2rem;
    }
    .start-info--text {
        padding: 40px 30px;
        border-top: 2px solid white;
        text-align: left;
    }
    .start-info--container .btn {
        margin-top: 40px;
    }
    .start-info--container {
        width: 90%;
        margin: auto;
    }
    .social-icons {
        position: relative;
    }
    .social-icons-left {
        left: 120px;
        bottom: 10px;
    }
    .icon {
        display: inline-block;
        background: #7DBFFF;
        width: 40px;
        height: 40px;
        border-radius: 50%;
        text-align: center;
        margin: 10px;
    }
    .icon:hover {
        background: white;
    }
    .icon--img {
        position: relative;
        vertical-align: middle;
        top: 6px;
    }
    .footer-mobile {
        display: none;
    }
    @media only screen and (max-width: 991px) {
        .start-info {
            width: 100%;
            top: 40%;
            border-left: none;
        }
        .footer {
            display: none;
        }
        .footer-mobile {
            display: block;
            border-top: 2px solid white;
            text-align: center;
            padding: 30px;
        }
    }
    @media only screen and (min-width: 992px) {
        .start-info--container {
            margin-right: 0;
            margin-left: auto;
        }
        .start-info--text {
            font-size: 1.3rem;
        }
    }
</style>
