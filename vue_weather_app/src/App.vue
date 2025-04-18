<script>
    import axios from 'axios'
    export default {
        data() {
            return {
                city: "",
                error: "",
                info: null
            }
        },
        computed: {
            cityName() {
                return "городе " + this.city
            },
            showTemp() {
                return "Сейчас: " + this.info.main.temp
            },
            showFeelsLike() {
                return "Ощущается: " + this.info.main.feels_like
            },
            showTempMin() {
                return "Минимум сегодня: " + this.info.main.temp_min
            },
            showTempMax() {
                return "Максимум сегодня: " + this.info.main.temp_max
            },
        },
        methods: {
            getWeather() {
                if(this.city.trim().length < 2) {
                    this.error = "Некорректно указан город"
                    return false
                }
                else {
                    this.error = ""

                    axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=756c3c4bc3bab24102880c3fbe2b4539`)
                        .then(res => (this.info = res.data))
                }
            }
        }
    }
</script>

<template>
    <div className="wrapper">
        <h1>Погода</h1>
        <p>Узнай погоду в {{ city == "" ? "твоем городе" : cityName }} </p>
        <div className="input_block">
            <input type="text" v-on:input="this.city = $event.target.value" placeholder="Укажите город">
            <button v-if="city != '' "@click="getWeather()">Узнать погоду</button>
            <button disabled v-else>Введите название города</button>
        </div>
        <p className="error">{{ error }}</p>
        <div className="weather_info" v-if="info != null">
            <p>{{ showTemp }}</p>
            <p>{{ showFeelsLike }}</p>
            <p>{{ showTempMin }}</p>
            <p>{{ showTempMax }}</p>
        </div>
    </div>
</template>

<style scoped>
    .wrapper {
        font-family: Arial, Helvetica, sans-serif;
        background-color: rgb(47, 0, 92);
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
    .input_block {
        min-height: 100px;
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
    .wrapper button:disabled {
        cursor: not-allowed;
        background: grey;
        transition: none;
    }
    .wrapper button:hover {
        border-bottom: 3px solid rgb(107, 0, 107);
        background: linear-gradient(110deg,rgba(83, 237, 219, 1) 0%, rgba(222, 92, 255, 1) 50%, rgba(87, 199, 115, 1) 100%);
        transform: translateY(-2px);
    }
    .error {
        margin-top: 50px;
        color: brown;
    }
</style>
