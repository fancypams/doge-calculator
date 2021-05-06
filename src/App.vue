<template>
  <div id="app">
    <div>
      <img src="https://upload.wikimedia.org/wikipedia/en/d/d0/Dogecoin_Logo.png">
      <h1>Here Doge-y Doge-y</h1>
    </div>
    <div class="wrap">
      <div class="card dark">
          <p>Dogecoin current USD value is:</p>
          <h3>${{ dogeValue }}</h3>
      </div>
      <div class="card">
        <h2>How many Doge-ies ya got?</h2>
        <p>Calculate what your Dogecoin is worth in USD</p>
        <input 
          id="dogeInput"
          v-model="numOfDoge"
          placeholder="# of Dogecoin">
        <button 
          @click="calculateDoge()"
          >
          Calculate
          </button>
        <h3 id="result">${{ userDogeValue }}</h3>
      </div>
    </div>
  </div>
    
</template>

<script>
import axios from 'axios'
export default {
  name: 'app',
  data () {
    return {
      dogeValue: '',
      numOfDoge: '',
      userDogeValue: 0
    }
  },
  mounted () {
    this.getDogePrice()
    setInterval(() => {
      this.getDogePrice()
    }, 10000)
  },
  methods: {
    getDogePrice() {
      axios
        .get('https://api.cryptonator.com/api/ticker/doge-usd')
        .then(response => {
            this.dogeValue = response.data.ticker.price
        })
    },
    calculateDoge() {
      this.userDogeValue = this.dogeValue * this.numOfDoge
    }
  }
}
</script>

<style lang="scss">
body {
  background-color: #d9a384;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  font-weight: bold;
  color: white;
}
button {
  border-radius: 10px;
  height: 35px;
  font-weight: bold;
  background-color: #2c3e50;
  color: white;
  border: none;
  text-transform: uppercase;
}
button:hover {
  background-color: white;
  color: #bf6b63;
}
input {
  height: 35px;
  border-radius: 10px;
  border: none;
  font-style: italic;
  padding: 0 0 0 15px;
}
input:focus {
  outline: gray 4px;
  outline-offset: 0;
  box-shadow: inset 0 0 0 2px
}
.wrap {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.card {
  border-radius: 25px;
  max-width: 350px;
  padding: 20px;
  margin: 5px;
  align-self: center;
}
.dark {
  background-color: #2c3e50;
  color: white;
  box-shadow: 5px 5px rgba(68, 68, 68, 0.2);
}
</style>
