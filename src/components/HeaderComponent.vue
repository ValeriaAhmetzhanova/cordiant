<template>
    <div class="header">
        <div class="header--item">
            <img src="../assets/logo.svg" alt="" height="20px">
        </div>
        <div class="header--item header--item-right">
            <img src="../assets/cordiant.svg" alt="" height="20px">
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