<template>
    <div class="header">
        <div class="header--item">
            ЛАЙФХАКЕР
        </div>
        <div class="header--item header--item-right">
            Cordiant
        </div>
    </div>
</template>

<script>
    export default {
        name: "Header"
    }
</script>

<style>
    .header {
        position: absolute;
        z-index: 5;
        padding: 30px;
        margin-bottom: 40px;
        width: 80%;
        left: 0;
        right: 0;
        margin-left: auto;
        margin-right: auto;
    }
    .header--item {
        display: inline-block;
        color: white;
        font-size: 2rem;
    }
    .header--item-right {
        float: right;
    }
</style>