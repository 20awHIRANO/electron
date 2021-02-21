<template>
  <div id="app">
    <div id = "all-area">
      <select v-model="selected">
        <option disabled value="">場所を選択</option>
        <option value="2128295">札幌</option>
        <option value="2129376">釧路</option>
        <option value="2113124">秋田</option>
        <option value="2111149">仙台</option>
        <option value="1855429">新潟</option>
        <option value="1850147">東京</option>
        <option value="1856057">名古屋</option>
        <option value="1853909">大阪</option>
        <option value="1862415">広島</option>
        <option value="1859146">高知</option>
        <option value="1863958">福岡</option>
        <option value="1856035">那覇</option>
      </select>
      <div id="chat-area">
        <p>今日は{{ weather }}で、気温は{{ temp }}度{{ end }}。</p>
      </div>
      <button v-on:click="getWeather()">天気を取得</button>
    </div>
    <router-view/>
  </div>
</template>

<script>
export default{
  name: "Template",
  data(){
    return{
    selected: '',
    weather: 'どんな天気',
    temp: '何',
    end: 'だろう',
    }
  },
  methods:{
    getWeather:function(){
      fetch('https://api.openweathermap.org/data/2.5/weather?id='+this.selected+'&units=metric&appid=e5019a35ffcb8a6eca2be87ffaaf0c3b',{
        method: "POST",
      })
      .then(response => response.json())
      .then(data => {
        this.weather = data.weather[0].main;
        this.temp = data.main.temp;
        this.end = "です";
      }).catch((error) => {
        console.error("Error",error)
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

