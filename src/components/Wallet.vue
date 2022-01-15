<template>
<div id="wallet">
  <div class="container py-4">
    <div class="row">
<!--      Wallets list-->
<!--      <div class="col-md-4 col-12">
        <ul class="list-group wallets-list">
          <li v-for="coin in availableCoins" @click="selectCoin(coin)" class="list-group-item" :class="{active:selectedCoin === coin}">
            {{ coin }}</li>
        </ul>
      </div>-->

<!--      Wallet content-->
      <div class="col-12">
        <div v-for="coin in availableCoins" class="card mb-2">
          <div class="card-header">
            {{coin}} Wallet
          </div>
          <div class="card-body">
            <h5 class="card-title">Your balance</h5>
            <p class="card-text">{{wallets[coin]}} {{coin}}</p>
            <p class="card-text" v-if="walletsConverted[coin] >= 0">{{walletsConverted[coin]}} USD</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: "Wallet",
  data(){
    return{
      wallets:{
        BTC:0.01,
        ETH:1.2,
        USDT:1600
      },
      walletsConverted:{
        BTC:-1,
        ETH:-1,
        USDT:-1
      },
      availableCoins:['BTC','ETH','USDT'],
      connection:null
    }
  },
  created() {
    this.$data.connection = new WebSocket('wss://streamer.cryptocompare.com/v2?api_key=559502082285f2c30ccf32d815bec78b3d57fd92637518f8b49567cdfa19af0d')
    this.$data.connection.onopen = (event)=>{
      console.log('Connected to WS')
      console.log(event)
      this.$data.connection.send(JSON.stringify({
        "action": "SubAdd",
        "subs": ["2~Coinbase~BTC~USD", "2~Coinbase~ETH~USD", "2~Coinbase~USDT~USD"]
      }))
    }
    this.$data.connection.onmessage = (event) =>{
      //console.log(JSON.parse(event.data))
      const data = JSON.parse(event.data)
      if (data.TYPE === "2"){
        console.log(data)
        if (typeof this.$data.walletsConverted[data.FROMSYMBOL] !== 'undefined' && typeof this.$data.wallets[data.FROMSYMBOL] !== 'undefined' && typeof data.PRICE !== 'undefined'){
          this.$data.walletsConverted[data.FROMSYMBOL] = data.PRICE * this.$data.wallets[data.FROMSYMBOL]
          this.$data.walletsConverted[data.FROMSYMBOL] = this.$data.walletsConverted[data.FROMSYMBOL].toFixed(2)
        }
      }
    }
  },
  unmounted() {
    this.$data.connection.close()
  }
}
</script>

<style scoped>
.wallets-list li{
  text-transform: uppercase;
}
</style>
