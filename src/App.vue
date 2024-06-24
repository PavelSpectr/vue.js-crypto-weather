<script>
import Input from "@/components/Input.vue";
import Selector from "@/components/Selector.vue";
import CryptoConvert from 'crypto-convert';
import Favorite from"@/components/Favorite.vue";

const convert = new CryptoConvert();

export default {
  components: {Input, Selector, Favorite},

  data() {
    return {
      amount: 0,
      cryptoFirst: '',
      cryptoSecond: '',
      error: '',
      result: 0,
      favs: []
    }
  },
  methods: {
    favorite() {
      this.favs.push({
        from: this.cryptoFirst,
        to: this.cryptoSecond
      })
    },
    getFromFavs(index) {
      this.cryptoFirst = this.favs[index].from
      this.cryptoSecond = this.favs[index].to
    },
    changeAmount(value) {
      this.amount = value
    },
    setCryptoFirst(value) {
      this.cryptoFirst = value
    },
    setCryptoSecond(value) {
      this.cryptoSecond = value
    },
    async convert() {
      if (this.amount <= 0) {
        return this.error = 'Number could not be less than 0';
      } else if (this.cryptoFirst == this.cryptoSecond) {
        return this.error = 'Chosen the same cuurencies';
      } else if (this.cryptoFirst == '' || this.cryptoSecond == '') {
        return this.error = 'Choose currency to compare';
      }
      this.error = '';

      await convert.ready();

      if(this.cryptoFirst == 'BTC' && this.cryptoSecond == 'ETH') {
        this.result = convert.BTC.ETH(this.amount);
      } else if(this.cryptoFirst == 'BTC' && this.cryptoSecond == 'USDT') {
        this.result = convert.BTC.USDT(this.amount);
      } else if(this.cryptoFirst == 'ETH' && this.cryptoSecond == 'BTC') {
        this.result = convert.ETH.BTC(this.amount);
      } else if(this.cryptoFirst == 'ETH' && this.cryptoSecond == 'USDT') {
        this.result = convert.BTC.USDT(this.amount);
      } else if(this.cryptoFirst == 'USDT' && this.cryptoSecond == 'BTC') {
        this.result = convert.USDT.BTC(this.amount);
      } else if(this.cryptoFirst == 'USDT' && this.cryptoSecond == 'ETH') {
        this.result = convert.USDT.ETH(this.amount);
      }
    }
  }
}
</script>

<template>
  <h1>Crypto</h1>

  <Input :changeAmount=changeAmount :convert="convert" :favorite="favorite" />
  <p v-if="error != ''">{{error}}</p>
  <p v-if="result != 0" className="result-text">{{result}}</p>
  <Favorite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs"/>
  <div className="selectors">
    <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst" />
    <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond"/>
  </div>

</template>

<style scoped>
  .selectors {
    display: flex;
    justify-content: space-around;
    width: 700px;
    margin: 0 auto;
  }
</style>
