<script>
import axios from "axios";
export default {
    data(){
      return{
        city: "",
        error: "",
        info: null
      }
    },
  computed:{
      cityName() {
        return "'" + this.city + "'"
      },
      showTemp() {
          return "Temperature: " + this.info.main.temp
      },
      showFeelsLike() {
        return "Temperature feels like: " + this.info.main.feels_like
      },
      showMinTemp() {
        return "Min.Temperature: " + this.info.main.temp_min
      },
      showMaxTemp() {
        return "Max.Temperature: " + this.info.main.temp_max
      },

  },
  methods:{
  getWeather() {
    if(this.city.trim().length<2){
      this.error ="Need more 1 symbol";
      return false;
    }

    this.error = ""

    axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=b172df1f516182179b4c10bc69fc507a`)
        .then(res => (this.info = res.data))
  }
  }
}
</script>

<template>
  <div class="wrapper">
    <h2>Weather checker</h2>
    <p>Find out the weather in {{ city == "" ? "your city" : cityName}}</p>
    <input type="text" v-model="city" placeholder="Enter city">
    <button v-if="city !== '' " @click="getWeather">Get weather</button>
    <button disabled v-else="city !== '' ">Enter data</button>
    <p class="error">{{ error }}</p>

    <div v-if="info != null">

      <p>{{showTemp}}</p>
      <p>{{showFeelsLike}}</p>
      <p>{{showMinTemp}}</p>
      <p>{{showMaxTemp}}</p>

    </div>

  </div>
</template>

<style scoped>
.error{
  color: red;
}

.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background: #1f0f24;
  text-align: center;
  color: aliceblue;
}
.wrapper h1{
margin-top: 50px;
}

.wrapper p{
  margin-top: 20px;
}

.wrapper input{
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}

.wrapper input:focus{
  border-bottom-color: #6e2d;
}
.wrapper button:disabled{
  background: darkgray;
  cursor: not-allowed;
  border: 2px solid dimgrey;
}

.wrapper button{
  background: chocolate;
  color: aliceblue;
  border-radius: 10px;
  border: 2px solid chocolate;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button:hover{
  transform: scale(1.1) translateY(-5px);
}
</style>
