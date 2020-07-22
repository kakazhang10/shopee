<template>
  <div id="app">
    <h1>Hello App!</h1>
      {{currency}} : {{rate}}
    <p>
      <router-link class='link' to="/">home</router-link>
      <router-link class='link' to="/about">about</router-link>
    </p>
    <router-view></router-view>
    <div>
      <HelloWorld msg="Welcome to Your Vue.js App"/>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
// import axios from 'axios'

export default {
  name: 'app',
  components: {
    HelloWorld
  },
  data () {
    return {
      rate: 0,
      currency: 'RMB'
    }
  },
  methods: {
    async getUSD () {
      const resData = await this.$http.get('https://api.coindesk.com/v1/bpi/currentprice.json')
      this.rate = resData.data.bpi.USD.rate
    },
    async getUSD2 () {
      const resData = await this.$http.fetch('https://api.coindesk.com/v1/bpi/currentprice.json')
      this.currency = resData.bpi.USD.code
    }
  },
  mounted () {
    this.getUSD()
    this.getUSD2()
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.link {
  margin-left: 1rem;
}
</style>
