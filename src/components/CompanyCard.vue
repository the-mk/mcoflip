<template>
  <div class="column animated fadeInUp faster">
    <div v-if="company" class="card">
    <div class="card-image has-text-centered">
        <img :src="require(`@/assets/${company.name}.png`)" :alt="company.name">
    </div>
      <div class="card-content has-text-centered">
        <p class="title"> {{ formatPrice(company.quotes.USD.market_cap) }} <i style="font-size: .45em; margin-left: .2em;" class="fas" :class="[{ 'fa-chevron-up': this.company.quotes.USD.percent_change_24h > 0 }, {'fa-chevron-down': this.company.quotes.USD.percent_change_24h < 0}]"><span style="margin-left: .4em">{{ this.company.quotes.USD.percent_change_24h.toFixed(2) }} %</span></i></p>
        <p class="subtitle">
          {{ company.name }} ({{ company.rank }}) 
        </p>
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
  import axios from 'axios';

  export default {
    name: 'companycard',
    data () {
      return {
        company: null,
      }
    },
    props: [
      'element'
    ],
    mounted () {
      axios
      .get('https://api.coinmarketcap.com/v2/ticker/' + this.element.id + '/?convert=USD')
      .then(response => this.company = response.data.data)
      .then(response => this.$emit('caps', [this.company.id, this.company.quotes.USD.market_cap]))
    },
    methods: {
      formatPrice(value) {
        let val = (value/1).toFixed(0).replace('.', ',')
        return '$ ' + val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")
      }
    }
  }
</script>

<style scoped lang="scss">
  img {
   height: 6em;
  }

  .card-image {
    padding-top: 8%;
  }

  .column {
    min-width: 300px;
  }

  .progressBorder {
    margin: 5em 0;
  }

  .fa-chevron-up {
    color: #27ae60;
  }

  .fa-chevron-down {
    color: #c0392b;
  }

  .fas > span {
    font-family: BlinkMacSystemFont,-apple-system,"Segoe UI",Roboto,Oxygen,Ubuntu,Cantarell,"Fira Sans","Droid Sans","Helvetica Neue",Helvetica,Arial,sans-serif;
  }
</style>