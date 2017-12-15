<template>
  <div class = "test">
  <div v-for ="n in 100" class="card card-1">
    <div>{{coinNames[n-1]}}</div>
    <div>{{coinSymbol[n-1]}}</div>
    <div>Coin Price in USD: {{coinPrice[n-1]}}</div>
    <div>Market Cap: {{marketCap[n-1]}}</div>
    <div>One Hour Change: {{change1hour[n-1]}}</div>
    <div>One Day Change: {{change24hour[n-1]}}</div>
    <div>One Week Change: {{change1week[n-1]}}</div>
  </div>
</div>
</template>

<script>
  export default {
    name: 'test',
    data() {
      return {
        coinNames: [],
        coinSymbol: [],
        rank: [],
        coinPrice: [],
        bitcoinPrice: [],
        marketCap: [],
        change1hour: [],
        change24hour: [],
        change1week: [],
        coinImg: [],
        maxSupply: [],
        totalSuply: []
      }
    },
    created: function() {
      this.$http.get('https://api.coinmarketcap.com/v1/ticker/')
        .then(function(response) {
          var datas = response.data;
          // console.log(datas);
          for (var i = 0; i < Object.keys(datas).length; i++) {
            this.coinNames[i] = datas[i].name;
            this.coinSymbol[i] = datas[i].symbol;
            this.rank[i] = datas[i].rank;
            this.coinPrice[i] = datas[i].price_usd;
            this.bitcoinPrice[i] = datas[i].price_btc;
            this.marketCap[i] = datas[i].market_cap_usd;
            this.change1hour[i] = datas[i].percent_change_1h;
            this.change24hour[i] = datas[i].percent_change_7d;
            this.change1week[i] = datas[i].percent_change_24h;
            this.totalSuply[i] = datas[i].total_supply;
            this.maxSupply[i] = datas[i].max_supply;
            // console.log(this.coinNames[i]);
          }
        })
    }
  }
</script>

<style scoped>
  .card {
    background: #fff;
    border-radius: 2px;
    display: inline-block;
    height: 300px;
    margin: 1rem;
    position: relative;
    width: 300px;
    margin-bottom: 10px;
  }

  .card-1 {
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
    transition: all 0.3s cubic-bezier(.25, .8, .25, 1);
  }

  .card-1:hover {
    box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  }
</style>
