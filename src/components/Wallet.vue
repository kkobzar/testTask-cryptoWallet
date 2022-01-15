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
      <div v-if="connection !== null" class="col-12">
        <div v-for="coin in availableCoins" class="card mb-2">
          <div class="card-header">
            {{coin}} Wallet
          </div>
          <div class="card-body">
            <h5 class="card-title">Your balance</h5>
            <p class="card-text">{{wallets[coin]}} {{coin}}</p>
            <p class="card-text" v-if="walletsConverted[coin] >= 0">{{walletsConverted[coin]}} &#36;</p>
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
      //get subs array for request
      let subs = []
      for (const coin of this.$data.availableCoins) {
        subs.push(`2~Coinbase~${coin}~USD`)
      }
      this.$data.connection.send(JSON.stringify({
        "action": "SubAdd",
        "subs": subs
      }))
    }
    this.$data.connection.onmessage = (event) =>{

      const data = JSON.parse(event.data)
      if (data.TYPE === "2"){
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
