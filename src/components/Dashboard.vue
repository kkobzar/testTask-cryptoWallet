<template>
<div id="dashboard">
  <div class="container">
    <div class="row">
      <div class="col-md-6 offset-md-3 col-12">
        <ul class="list-group dashboard-pair-select-menu">
          <li class="list-group-item list-group-item-action" :class="{active:selectedCoin==='BTC'}">
            <button @click="switchPair('BTC')" class="btn btn-success">btc/usd</button></li>
          <li class="list-group-item list-group-item-action" :class="{active:selectedCoin==='ETH'}">
            <button @click="switchPair('ETH')" class="btn btn-primary">eth/btc</button></li>
        </ul>
      </div>
    </div>
    <!-- TradingView Widget BEGIN -->
    <div class="tradingview-widget-container">
      <div id="tradingview_004f2"></div>
      <div class="tradingview-widget-copyright"><a href="https://ru.tradingview.com/symbols/BTCUSD/?exchange=BINANCEUS" rel="noopener" target="_blank"><span class="blue-text">График BTCUSD</span></a> от TradingView</div>

    </div>
    <!-- TradingView Widget END -->
  </div>

</div>
</template>

<script>
export default {
  name: "Dashboard",
  data(){
    return{
      selectedCoin:'BTC',
      tvWidget: null
    }
  },
  mounted() {
    this.$data.tvWidget = new TradingView.widget(
        {
          "width": 890,
          "height": 610,
          "symbol": "BINANCEUS:BTCUSD",
          "interval": "1H",
          "timezone": "Etc/UTC",
          "theme": "light",
          "style": "1",
          "locale": "en",
          "toolbar_bg": "#f1f3f6",
          "enable_publishing": false,
          "allow_symbol_change": true,
          "container_id": "tradingview_004f2"
        }
    );
  },
  methods:{
    switchPair(coin){
      if (!coin || this.$data.tvWidget === null)
        return

      this.$data.selectedCoin = coin
      this.$data.tvWidget.options.symbol =  `BINANCEUS:${coin}USD`
    }
  }
}
</script>

<style scoped>

</style>
