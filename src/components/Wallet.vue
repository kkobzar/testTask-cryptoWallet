<template>
<div id="wallet">
  <div class="container py-4">
    <div class="row">
<!--      Wallets list-->
      <div class="col-md-4 col-12">
        <ul class="list-group wallets-list">
          <li v-for="coin in avaliableCoins" @click="selectCoin(coin)" class="list-group-item" :class="{active:selectedCoin === coin}">
            {{ coin }}</li>
        </ul>
      </div>

<!--      Wallet content-->
      <div class="col-md-8 col-12">
        <div class="card">
          <div class="card-header">
            {{selectedCoin}} Wallet
          </div>
          <div class="card-body">
            <h5 class="card-title">Your balance</h5>
            <p class="card-text"></p>
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
      avaliableCoins:['BTC','ETH','USDT'],
      selectedCoin:'BTC',
      connection:null
    }
  },
  methods:{
    selectCoin(coin){
      this.$data.selectedCoin = coin
    }
  },
  created() {
    /*this.$data.connection = new WebSocket('wss://streamer.cryptocompare.com/v2?api_key=559502082285f2c30ccf32d815bec78b3d57fd92637518f8b49567cdfa19af0d')
    this.$data.connection.onopen = (event)=>{
      console.log('Connected to WS')
      console.log(event)
      this.$data.connection.send(JSON.stringify({
        "action": "SubAdd",
        "subs": ["2~Coinbase~BTC~USD"]
      }))
    }
    this.$data.connection.onmessage = (event) =>{
      console.log(JSON.parse(event.data))
    }*/
  }
}
</script>

<style scoped>
.wallets-list li{
  text-transform: uppercase;
}
</style>
