<template>
  <v-app dark class="blue-grey darken-3">
    <!--{{singapore}}-->
    <!--{{happy}}-->
    {{hongkong}}
    {{sad}}
    <v-card>
    {{supply}}
    </v-card>
    <v-card>
    {{base}}
    </v-card>
    <v-card>
    {{quote}}
    </v-card>

  </v-app>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'Singapore',
    data () {
      return {
        singapore: 'Xinjiapo',
        hongkong: 'Xianggang',
        klpmarket: [],
        supply: '',
        base: '',
        quote: ''
      }
    },
    created () {
      this.singapore = '100'
    },
    computed: {
      happy: function () {
        axios
          .post('http://api-kylin.eosasia.one/v1/chain/get_info')
          .then(response => (this.singapore = response.data))
        return this.singapore
      },
      sad: function () {
        axios
          .post('http://api-kylin.eosasia.one/v1/chain/get_table_rows', {
            'code': 'eoshenzhensg',
            'scope': 'eoshenzhensg',
            'table': 'klpmarket',
            'json': 'true'
          })
          .then(response => (this.hongkong = response.data))
        this.klpmarket = this.hongkong.rows
        console.log('this.hongkong.rows', this.hongkong)
        this.supply = this.klpmarket[0].supply
        this.base = this.klpmarket[0].base.balance
        this.quote = this.klpmarket[0].quote.balance
        console.log('supply', this.supply)
        return this.hongkong
      }
    },
    beforeDestroy () {

    }
  }
</script>

<style scoped>

</style>
