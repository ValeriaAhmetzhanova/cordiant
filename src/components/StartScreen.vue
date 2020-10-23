<template> 
    <div>
        <div class="header">
            <div class="header--item">
                ЛАЙФХАКЕР
            </div>
            <div class="header--item header--item-right">
                Cordiant
            </div>
        </div>
        <div>
            <div class="body">
                <div class="body--title">
                    Узнаете ли вы Россию
                    <br>
                    <strong>ПО ДОРОГАМ?</strong>
                </div>
                <div class="body--text">
                    Мы составили этот тест вместе с производителем шин Cordiant,
                    чтобы вы проверили, сможете ли отличить российские дороги
                    от остальных. Активируйте внутреннего Шерлока — и вперёд!
                    Пройдёте тест до конца — получите скидку 15% на зимнюю резину.
                    <div class="btn"
                         v-on:click="$emit('startQuiz')">
                        Пройти тест!
                    </div>
                </div>
            </div>
        </div>
        <div class="footer">
            <div class="social-icons">
                <div class="icon"><img class="icon--img" src="../assets/twitter.svg" alt=""></div>
                <div class="icon"><img class="icon--img" src="../assets/vk.svg" alt=""></div>
                <div class="icon"><img class="icon--img" src="../assets/fb.svg" alt=""></div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "StartScreen"
    };
</script>

<style>
    #start {
        background: url("../assets/start-background.png") no-repeat center center fixed;
        -webkit-background-size: cover;
        -moz-background-size: cover;
        -o-background-size: cover;
        background-size: cover;
        box-shadow: inset 10px 10px 20px black;
        height: 100vh;
    }
    .header {
        padding: 30px;
        margin-bottom: 40px;
    }
    .header--item {
        display: inline-block;
        color: white;
        font-size: 2rem;
    }
    .header--item-right {
        float: right;
    }
    .body {
        width: 50%;
        background: #004373;
        text-align: center;
        color: white;
        border: 2px solid white;
        border-right: none;
        margin-left: auto;
        margin-right: 0;
    }
    .body--title {
        padding: 30px;
        border-bottom: 2px solid white;
        margin-bottom: 8px;
        font-size: 2rem;
    }
    .body--text {
        padding: 30px;
        border-top: 2px solid white;
        font-size: 1.5rem;
    }
    .footer {
        position: fixed;
        padding: 30px;
        bottom: 0;
    }
    .social-icons {
        position: relative;
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
    .icon--img {
        position: relative;
        vertical-align: middle;
        top: 10px;
    }
</style>
