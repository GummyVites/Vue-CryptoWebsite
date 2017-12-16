<template>
  <div class = "test">
  <div class="search-wrapper">
    <input type="text" v-model="search" placeholder="Search Coin Symbol"/>
  </div>
  <div v-if = "search !='' " v-for ="item in filteredName" icon="search" class="card card-1">
    <div>{{item.name}}</div>
    <div>{{item.symbol}}</div>
    <div>Coin Price in USD: ${{item.price_usd}}</div>
    <div>Bitcoin Price: {{item.price_btc}}</div>
    <div>Market Cap: {{item.market_cap_usd}}</div>
    <div>One Hour Change: {{item.percent_change_1h}}</div>
    <div>One Day Change: {{item.percent_change_7d}}</div>
    <div>One Week Change: {{item.percent_change_24h}}</div>
  </div>

  <div v-else v-for ="n in 100" class="card card-1">
    <div>{{coinNames[n-1]}}</div>
    <div>{{coinSymbol[n-1]}}</div>
    <div>Coin Price in USD: ${{coinPrice[n-1]}}</div>
    <div>Bitcoin Price: {{bitcoinPrice[n-1]}}</div>
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
    computed:{
      filteredName:function(){
          return this.coins.filter((item) => {
             return item.symbol.toUpperCase().includes(this.search.toUpperCase());
          });
          // }
        }
      },
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
        totalSuply: [],
        coins: [],
        search: ''
      }
    },
      created: function() {
      this.$http.get('https://api.coinmarketcap.com/v1/ticker/')
        .then(function(response) {
          var datas = response.data;
          this.coins = response.data;
          // console.log(this.coins);

          for (var i = 0; i < Object.keys(datas).length; i++) {
            this.$set(this.coinNames, i, datas[i].name)
            this.$set(this.coinSymbol, i, datas[i].symbol)
            this.$set(this.rank, i, datas[i].rank)
            this.$set(this.coinPrice, i, datas[i].price_usd)
            this.$set(this.bitcoinPrice, i, datas[i].price_btc)
            this.$set(this.marketCap, i, datas[i].market_cap_usd)
            this.$set(this.change1hour, i, datas[i].percent_change_1h)
            this.$set(this.change24hour, i, datas[i].percent_change_7d)
            this.$set(this.change1week, i, datas[i].percent_change_24h)
            this.$set(this.totalSuply, i, datas[i].total_supply)
            this.$set(this.maxSupply, i, datas[i].max_supply)
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

  .search-wrapper{
    margin: 10px 0;
  }

  input {
    width: 400px;
    height: 20px;

}
</style>
