<script>
import axios from 'axios' // импортируем компонент который добавляет возможность подтягивать данные со стороннего API (команда: npm i axios)

export default {  // задаём и экпортируем переменные основной в код
data() {
  return {
    city:"",
    error:"",
    info: null
  }
},
computed: {     // получаем определенные данные с помощью функции с изменением
   cityName() {
    return "-"+ this.city + "-"
   },
   showTemp(){
    return "Tемпература: " +this.info.main.temp
   },
   showFeelsLike(){
    return "Ощущается как: " +this.info.main.feels_like
   },
   showMinTemp(){
    return "Tемпература (мин): " +this.info.main.temp_min
   },
   showMaxTemp(){
    return "Tемпература (макс): " +this.info.main.temp_max
   },
},


methods:{  // проверка на ошибки c условием если ошибки по длине нет то считывай и возвращай
  getWeather(){
    if(this.city.trim().length <2){
      this.error = "Введите больше 1 символа"
     return false
    }
    this.error = "" 
    axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=4a1a8e2c30917dc57f2d405e5e5e1028`)
    .then(res => (this.info = res.data))
  }
 }
}
</script>

<template>   
 <div class="wrapper">  
  <h1>Погода</h1>
  <p>Узнать погоду в {{ city =="" ? " вашем населённом пункте": cityName}}</p>
  <input type="text" v-model = "city" placeholder="Введите город">
  <button v-if="city !=''" @click="getWeather()">Получить погоду</button>
  <button disabled v-else>Введите название города</button>
  <p class="error">{{ error }}</p>
  
  <div v-if="info != null">
    <p>{{ showTemp }}</p>
    <p>{{ showFeelsLike }}</p>
    <p>{{ showMinTemp }}</p>
    <p>{{ showMaxTemp }}</p>

  </div>
  
  
 
 </div>
</template>

<style scoped>
.error{
  color: red;
}
.wrapper{
  width: 1000;
  height: 600px;
  border-radius: 70;
  padding: 40px;
  text-align: center;
  color: aliceblue;
}

.wrapper h1{
  margin-top: 50px;
}

.wrapper p{
  margin-top: 50px;
}
.wrapper button{
  background: red;
  color: chocolate;
  border-radius: 10px;
  border: 2px solid firebrick;
  padding: 11px 12px;
  margin-left: 10px;
  cursor: pointer;
  transition: transform 500ms ease;
}
.wrapper button:hover{
  transform: scale(1,1) translateY(+3px);
}

.wrapper button :disabled{
  background-color: darkslategray;
  cursor: not-allowed;

}
.wrapper input{
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 3px solid black;
  color: azure;
  font-size: 14px;
  padding: 6px 8px;
  outline: none;
}
.wrapper input:focus{
  border-bottom-color: green;
}

</style>

