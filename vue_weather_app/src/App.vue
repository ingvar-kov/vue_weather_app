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
                return this.info.main.temp
            },
            showFeelsLike() {
                return this.info.main.feels_like
            },
            showTempMin() {
                return this.info.main.temp_min
            },
            showTempMax() {
                return this.info.main.temp_max
            },
        },
        methods: {
            getWeather() {
                axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=756c3c4bc3bab24102880c3fbe2b4539`)
                        .then(res => (this.info = res.data))

                if(this.info == null) {
                    this.error = "Некорректно указан город"
                    return false
                }
                else {
                    this.error = ""
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
        <p className="error" v-if="info == null">{{ error }}</p>
        <div className="weather_info" v-if="info != null">
            <div className="weather_field">
                <p>Сейчас:</p>
                <p>{{ showTemp }} °С</p>
            </div>
            <div className="weather_field">
                <p>Ощущается:</p>
                <p>{{ showFeelsLike }} °С</p>
            </div>
            <div className="weather_field">
                <p>Минимум сегодня:</p>
                <p>{{ showTempMin }} °С</p>
            </div>
            <div className="weather_field">
                <p>Максимум сегодня:</p>
                <p>{{ showTempMax }} °С</p>
            </div>
        </div>
    </div>
</template>

<style scoped>
    template {
        display: flex;
        justify-content: center; /* центрирование по главной оси (горизонтально) */
        align-items: center;     /* центрирование по поперечной оси (вертикально) */
        height: 100vh;
    }
    .wrapper {
        font-family: Arial, Helvetica, sans-serif;
        background-color: rgb(47, 0, 92);
        width: 766px;
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
        margin-bottom: 45px;
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
    .weather_field {
        width: 390px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        box-sizing: border-box;
        margin-left: auto;
        margin-right: auto;
        margin-bottom: 20px;
        padding: 10px;
        line-height: 1;
        font-size: 18px;
        border-radius: 10px;
        background: linear-gradient(110deg,rgb(47, 0, 92) 45%, rgba(87, 199, 115, 1) 85%, rgb(131, 255, 241) 100%);
        color: rgb(47, 0, 92);
        text-align: center;
    }
    .weather_field p {
        margin: 0;
        padding: 0;
    }
    .weather_field p:first-child {
        color: white;
    }
    .weather_field p:last-child {
        font-weight: 700;
    }
    @media (max-width: 768px) {
        .wrapper {
            width: 90vw;
            margin-top: 5vw;
            margin-bottom: 5vw;
        }
        .weather_field {
            width: 80%;
        }
    }
    @media (max-width: 550px) {
        .input_block {
            width: 80%;
            margin: auto;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            margin-bottom: 40px;
            margin-top: 20px;
        }
        .input_block input {
            box-sizing: border-box;
            margin: auto;
            width: 90%;
        }
        .input_block button {
            box-sizing: border-box;
            margin: auto;
            width: 90%;
        }
    }
    @media (max-width: 424px) {
        .weather_field p {
            font-size: 14px;
        }
    }
</style>
