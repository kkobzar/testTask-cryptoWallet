<template>
<div id="dashboard">
  <div class="container pt-4">
    <div class="row pb-2">
      <div class="col-md-6 offset-md-3 col-12">
        <h2>Choose coin pair</h2>
        <ul class="list-group dashboard-pair-select-menu">
          <li class="list-group-item list-group-item-action" :class="{active:selectedCoin==='BTC'}" @click="switchPair('BTC')">
            btc/usd</li>
          <li class="list-group-item list-group-item-action" :class="{active:selectedCoin==='ETH'}" @click="switchPair('ETH')">
            eth/btc</li>
        </ul>
      </div>
    </div>
    <div class="row">
      <div class="col-12">
        <!-- TradingView Widget BEGIN -->
        <div class="tradingview-widget-container">
          <div id="tradingview_004f2"></div>
          <div class="tradingview-widget-copyright"><a :href="'https://ru.tradingview.com/symbols/'+selectedCoin+'USD/?exchange=BINANCEUS'" rel="noopener" target="_blank"><span class="blue-text">График {{selectedCoin}}USD</span></a> от TradingView</div>
        </div>
        <!-- TradingView Widget END -->
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: "Dashboard",
  data(){
    return{
      selectedCoin:'BTC',
      tvWidget: null,
      tvWidgetOptions:{
        "width": 890,
        "height": 610,
        "interval": "1H",
        "timezone": "Etc/UTC",
        "theme": "light",
        "style": "1",
        "locale": "en",
        "toolbar_bg": "#f1f3f6",
        "enable_publishing": false,
        "allow_symbol_change": false,
        "container_id": "tradingview_004f2"
      }
    }
  },
  mounted() {
    this.$data.tvWidget = new TradingView.widget(
        {...this.$data.tvWidgetOptions,"symbol":"BINANCEUS:BTCUSD"}
    )
  },
  methods:{
    switchPair(coin){
      if (!coin || this.$data.tvWidget === null)
        return

      //Couldn't set symbol so just reload widget
      // https://github.com/serdimoa/charting/blob/master/Widget-Methods.md#setsymbolsymbol-interval-callback
      this.$data.selectedCoin = coin
      this.$data.tvWidget = new TradingView.widget(
          {...this.$data.tvWidgetOptions,"symbol":`BINANCEUS:${coin}USD`}
      )
    }
  }
}
</script>

<style scoped>

</style>
