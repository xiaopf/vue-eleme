<template>
  <div id="app">
     <vheader :seller="seller"></vheader>
     <vtab v-bind:minPrice="seller.minPrice" v-bind:deliveryPrice="seller.deliveryPrice"></vtab>
  </div>
</template>

<script type="text/ecmascript-6">
    import header from './components/header/header';
    import tab from './components/tab/tab';
    import Vue from 'vue';
    import axios from 'axios';
    import VueAxios from 'vue-axios';

    Vue.use(VueAxios, axios);

    export default {
      data () {
          return {
            seller: {}
          };
      },
      created () {
          Vue.axios.get('http://localhost:8080/api/seller').then((response) => {
            this.seller = response.data.data;
          });
      },
      components: {
          vheader: header,
          vtab: tab
      }
    };

</script>

<style>
   #app{
    width: 100%;
    height: 100%;
    overflow: hidden;
   }
</style>
