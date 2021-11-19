<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''">
    <main>
    <div class="climaBox" v-if="typeof weather.main != 'undefined'">
      <div class="lugar-session">
          <div class="local">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="data">Follow me - github.com/TLucas97</div>
      </div>

      <div class="clima-session">
        <div class="temperatura">{{ Math.round(weather.main.temp) }}ºC</div>
        <div class="weather"> {{ weather.weather[0].main }} </div>
      </div>
    </div>
      <div class="caixa-de-pesquisa">
        <input type="text" class="text-pesquisa" placeholder="Em que local você está?" v-model="query" @keypress="climaMethod">
      </div>
   
    </main>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      api_key: '8d97c89bb6b2e3e3d3b6b6366b57cdda',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
    methods: {
      climaMethod (e){
        if(e.key == "Enter") {
          fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }) .then(this.setResults);
        }
      },
      setResults (results) {
        this.weather = results;
      }
    },


}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Oswald:wght@200;400;700&display=swap');

  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body{
    font-family: Arial, Helvetica, sans-serif;
  }

  #app{
    background: url('./assets/weatherBG.jpg');
    background-size: cover;
    background-position: bottom;
    transition: 0.4s
  }

  #app.warm {
    background: url('./assets/warmBG.jpg');
    background-size: cover;
    background-position: bottom;
  }

  main{
    min-height: 100vh;
    padding: 25px;

    background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
  }

  .caixa-de-pesquisa{
    width: 100%;
    margin-bottom: 30px;
  }

  .caixa-de-pesquisa .text-pesquisa{
    display: block;
    width: 100%;
    padding: 35px;
    margin-top: 20%;

    color: black;
    font-size: 25px;

    appearance: none;
    border: none;
    background: none;
    outline: none;

    box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: 16px 0px 16px 0px;
    transition: 0.6s;
  }

  .caixa-de-pesquisa .text-pesquisa:focus{
    box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.75);
    background-color: rgba(255, 255, 255, 0.75);
    border-radius: 0px 16px 0px 16px;
  }

  .lugar-session .local{
    text-align: center;
    font-size: 40px;
    font-weight: bold;
    color: white;
    font-family: 'Oswald', sans-serif;
    letter-spacing: 5.6px;
  }

  .lugar-session .data{
    text-align: center;
    font-size: 25px;
    font-weight: 600;
    color: white;
    font-family: 'Oswald', sans-serif;
  }

  .clima-session{
    margin-top: 30px;
    text-align: center;
  }

  .clima-session .temperatura{
    display: inline-block;
    font-size: 100px;
    font-weight: bold;
    color: rgba(255, 255, 255, 0.76);
    font-family: 'Oswald', sans-serif;
    letter-spacing: 5.6px;

    text-shadow: 1px 7px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.322);
    border-radius: 20px;
    padding: 15px;
    box-shadow: 1px 7px rgba(0, 0, 0, 0.25);
  }

  .clima-session .weather{
    text-align: center;
    font-size: 35px;
    font-weight: bold;
    color: white;
    font-family: 'Oswald', sans-serif;
    letter-spacing: 5.6px;
  }

</style>
