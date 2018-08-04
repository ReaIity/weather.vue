<template>
    <div class="wrap">{{name}}
     <!-- <button v-on:click="click" class="button">{{button}}</button>-->
      <select v-on:change="change" class="select">
        <option v-for="item in city" v-bind:value="item"
                :key="item">{{item}}</option>
        <!--<option selected value="Moscow">Москва</option>
        <option value="Volgograd">Волгоград</option>
        <option value="Penza">Пенза</option>-->
      </select>
      <div class="plus" v-on:click="onclick">+</div>
      <div class="forecast" id="forecast"></div>
    </div>
</template>

<script>/* eslint-disable */
  // eslint-disable-next-line
export default {
  name: 'test',
  data () {
    return {
      name: 'Погода',
      button: 'Кнопка',
      message: 'Вы загрузили эту страницу в: ' + new Date().toLocaleString(),
      city: ['Moscow', 'Volgograd', 'Penza']
    }
  },

  mounted () {
    this.getData ()

  },
  methods: {
    getData () {
      var url = 'https://api.openweathermap.org/data/2.5/weather?q=Moscow&appid=68b26f6d3fbcc173eed1b628a08ee439';
      reloadForecast()
      showForecast (url)
      function reloadForecast() {
        var forecast = document.getElementById('forecast');
        forecast.innerHTML = ''

      }
      function showForecast (url) {
        var arr =  getRequest(url),
          forecast = document.getElementById('forecast'),
          i;
        for (i = 0; i <= arr.length; i++) {
          if (i == 0) {
            var city = document.createElement('p');
            city.innerHTML = arr[0]
            forecast.appendChild(city)
          } else if (i == 1) {
            var temp = document.createElement('p');
            temp.innerHTML = arr[1]
            forecast.appendChild(temp)
          } else if (i == 2) {
            var press = document.createElement('p');
            press.innerHTML = arr[2]
            forecast.appendChild(press)
          }
        }

      }
      function getRequest(url) {
        var xhr = new XMLHttpRequest()
        xhr.open('GET', url, false )
        xhr.send()
        if (xhr.status != 200) {
          console.log('Ошибка ' + xhr.status + ': ' + xhr.statusText)
        }
        else {
          var answer = JSON.parse(xhr.responseText),
            arr = [],
            name = 'name',
            pressure = 'pressure',
            temp = 'temp';
          translateCity(answer)
          arr.push(answer[name])
          arr.push(getTemperature(answer))
          arr.push(getPressure(answer))
          return arr
          function translateCity(answer) {
            var name = 'name';
            if (answer[name] == 'Moscow') {
              answer[name] = 'Москва'
            } else if (answer[name] == 'Volgograd') {
              answer[name] = 'Волгоград'
            } else if (answer[name] == 'Penza') {
              answer[name] = 'Пенза'
            }
            return answer[name]
          }
        }

        function getTemperature(answer) {
          var main = 'main',
            obj = {},
            temp = 'temp',
            temperature;
          obj = answer[main]
          temperature = obj[temp]
          temperature =  changeTemperature(temperature)
          return temperature
        }
        function changeTemperature(temperature) {
          var temp = '',
            t = temperature - 273,
            res,
            result;
          temp = temp + t
          res = temp.split('.', 1)
          result = res[0] + '&#176; C'
          return result
        }
        function getPressure(answer) {
          var main = 'main',
            obj = {},
            pressure = 'pressure',
            press;
          obj = answer[main]
          press = obj[pressure]
          press = changePressure(press)
          return press

          function changePressure(press) {
            var pres = press * 0.75 ,
              res = '',
              r;
            res = res + pres
            r = res.split('.', 1)
            return r[0] + ' мм. рт. ст'
          }
        }
      }
    },

    click (e) {
      console.log(e.target)
    },

    change (e) {
      var url = 'https://api.openweathermap.org/data/2.5/weather?q=' + e.target.value + '&appid=68b26f6d3fbcc173eed1b628a08ee439';
        reloadForecast()
        showForecast (url)
      function reloadForecast() {
          var forecast = document.getElementById('forecast');
          forecast.innerHTML = ''

      }
      function showForecast (url) {
       var arr =  getRequest(url),
         forecast = document.getElementById('forecast'),
         i;
       for (i = 0; i <= arr.length; i++) {
         if (i == 0) {
           var city = document.createElement('p');
           city.innerHTML = arr[0]
           forecast.appendChild(city)
         } else if (i == 1) {
           var temp = document.createElement('p');
           temp.innerHTML = arr[1]
           forecast.appendChild(temp)
         } else if (i == 2) {
           var press = document.createElement('p');
           press.innerHTML = arr[2]
           forecast.appendChild(press)
         }
       }

      }
      function getRequest(url) {
        var xhr = new XMLHttpRequest()
        xhr.open('GET', url, false )
        xhr.send()
        if (xhr.status != 200) {
          console.log('Ошибка ' + xhr.status + ': ' + xhr.statusText)
        }
        else {
          var answer = JSON.parse(xhr.responseText),
            arr = [],
            name = 'name',
            pressure = 'pressure',
            temp = 'temp';
          translateCity(answer)
          arr.push(answer[name])
          arr.push(getTemperature(answer))
          arr.push(getPressure(answer))
          return arr
          function translateCity(answer) {
            var name = 'name';
            if (answer[name] == 'Moscow') {
              answer[name] = 'Москва'
            } else if (answer[name] == 'Volgograd') {
              answer[name] = 'Волгоград'
            } else if (answer[name] == 'Penza') {
              answer[name] = 'Пенза'
            }
            return answer[name]
          }
        }

        function getTemperature(answer) {
          var main = 'main',
            obj = {},
            temp = 'temp',
            temperature;
          obj = answer[main]
          temperature = obj[temp]
          temperature =  changeTemperature(temperature)
          return temperature
        }
        function changeTemperature(temperature) {
          var temp = '',
            t = temperature - 273,
            res,
            result;
          temp = temp + t
          res = temp.split('.', 1)
          result = res[0] + '&#176; C'
          return result
        }
        function getPressure(answer) {
          var main = 'main',
            obj = {},
            pressure = 'pressure',
            press;
          obj = answer[main]
          press = obj[pressure]
          press = changePressure(press)
          return press

          function changePressure(press) {
            var pres = press * 0.75 ,
              res = '',
              r;
            res = res + pres
            r = res.split('.', 1)
            return r[0] + ' мм. рт. ст'
          }
        }
      }
    },

    onclick (e) {
      var select = document.querySelector('select'),
        newOption = document.createElement('option');
      createOption(newOption)
      select.appendChild(newOption)
      function createOption(newOption) {
        var modulWindow = document.createElement('div'),
          wrap = document.getElementsByClassName('wrap'),
          plus = wrap[0];
        modulWindow.innerHTML = 'rrrr'
        //classList.add
        plus.appendChild(modulWindow)
      }
    }
  }
}
</script>

<style scoped>
  .wrap {
    margin: auto;
    text-align: center;

  }
  .button {
    width: 100px;
    border-radius: 5px;
    background: blue;
    color: white;
  }
  .select {
    background: deepskyBlue;
    color: white;
    border-radius: 7px;
    border: 0px solid white;
    text-align-last: center;
    width: auto;
    min-width: 120px;
  }
  .forecast {
    border-radius: 7px;
    min-width: 250px;
    position: absolute;
    left: 50%;
    top: 15%;
    transform: translate(-50%, -85%);
    border: 1px solid lightskyblue;
    width: auto;
    height: auto;
    min-height: 100px;
    text-align: center;
    vertical-align: middle;
    pointer-events: none;
  }

  .plus {
    /*position: absolute;
    left: 59.5%;
    top: 0;*/
    width: 15px;
    height: auto;
    cursor: pointer;
    font-size: 125%;

  }
  .plus:hover {
    color: darkslateblue;
    font-size: 175%;
    font-weight: 600;
    top: 1px;
    text-align: center;
  }
</style>
