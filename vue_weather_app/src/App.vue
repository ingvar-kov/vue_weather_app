<script setup>

</script>

<template>
    <div className="wrapper">
        <h1>School 21 Погода</h1>
        <p>Узнай погоду в твоем городе!</p>
        <input type="text" placeholder="Укажите город">
        <button>Узнать погоду</button>
    </div>
</template>

<style scoped>
    .wrapper {
        background-color: blueviolet;
        width: 900px;
        height: 500px;
        border-radius: 20px;
        text-align: center;
        color: white;
        padding-top: 40px;
    }
    .wrapper p {
        margin-top: 10px;
    }
    .wrapper input {
        margin-top: 20px;
    }
    .wrapper button {
        margin-left: 5px;
    }
</style>
