<template>
<!-- можно удалить v-bind? -->
  <div class="v-catalog v-catalog__list"> {{  }}
      <v-catalog-item
      v-for="product in PRODUCTS"
       :key="product.article"
       v-bind:product_data="product"
       @sendDataToPArent="showChildArticleConsole"
        />
  </div>
  
</template>

<script>
import vCatalogItem from './v-catalog-item'
import {mapActions} from 'vuex'
import {mapGetters} from 'vuex'    

export default {
  name: 'v-catalog',
  components:{
      vCatalogItem,
  },
  
  data() {
    return{
     
    }

  },

computed: {
  ...mapGetters([
     'PRODUCTS'
  ]),
},
methods: {
  ...mapActions([
    'GET_PRODUCTS_FROM_API'
  ]),
   showArticleConsole(data){
       console.log(data);
     }
 },
 mounted(){
   this.GET_PRODUCTS_FROM_API()
   .then((response) => {
     if(response.data){
       console.log('Data Arrive');
     }
   })
 }
}
</script>

<style lang="scss">
  .v-catalog {
    &__list {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
    }
    &__link_to_cart {
      position: fixed;
      top: 80px;
      right: 10px;
      padding: $padding*2;
      border: solid 1px #aeaeae;
      background: #ffffff;
    }
  }
  .filters {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .range-slider {
    width: 200px;
    margin: auto 16px;
    text-align: center;
    position: relative;
  }
  .range-slider svg, .range-slider input[type=range] {
    position: absolute;
    left: 0;
    bottom: 0;
  }
  input[type=range]::-webkit-slider-thumb {
    z-index: 2;
    position: relative;
    top: 2px;
    margin-top: -7px;
  }
</style>