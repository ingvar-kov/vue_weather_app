<script>
    export default {
        data() {

        }
    }
</script>

<template>
    <div className="wrapper">
        <h1>School 21 - Погода</h1>
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
        border-radius: 30px;
        text-align: center;
        color: white;
        padding-top: 40px;
    }
    .wrapper p {
        margin-top: 10px;
    }
    .wrapper input {
        outline: none;
        border: none;
        padding: 5px 10px;
        margin-top: 40px;
        font-size: 18px;
        border-radius: 10px;
        cursor: pointer;
        transition: transform 200ms ease;
    }
    .wrapper input:focus {
        border: none;
        outline: none;
        border-bottom: 3px solid rgb(14, 173, 0);
        transform: translateY(-2px);
    }
    .wrapper button {
        color: azure;
        text-shadow: 1px 1px 3px rgb(82, 0, 68);
        border: none;
        padding: 5px 10px;
        margin-left: 15px;
        font-size: 18px;
        border-radius: 10px;
        background: linear-gradient(110deg,rgba(222, 92, 255, 1) 0%, rgba(87, 199, 115, 1) 50%, rgba(83, 237, 219, 1) 100%);
        cursor: pointer;
        transition: transform 200ms ease-in;
    }
    .wrapper button:hover {
        border-bottom: 3px solid rgb(107, 0, 107);
        background: linear-gradient(110deg,rgba(83, 237, 219, 1) 0%, rgba(222, 92, 255, 1) 50%, rgba(87, 199, 115, 1) 100%);
        transform: translateY(-2px);
    }
</style>
