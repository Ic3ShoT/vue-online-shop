<template>
  <div class="v-catalog">
    <h1 class="v-catalog__header">Catalog:</h1>
    <router-link :to="{name: 'cart', params: {cart_data: CART}}">
      <div class="v-catalog__link_to_cart">
        Cart: {{CART.length}}
      </div>
    </router-link>
    <router-link :to="{name: 'profile', params: {cart_data: CART}}">
      <div class="v-catalog__link_to_profile">
        Profile
      </div>
    </router-link>
    <v-catalog-item
      v-for="product in PRODUCTS"
      :key="product.article"
      :product_data="product"
      @addToCart="addToCart"
    />
 </div>
</template>

<script>
import vCatalogItem from './v-catalog-item'
import {mapActions, mapGetters} from 'vuex'
export default {
  name: "v-catalog",
  components:{
    vCatalogItem
  },
  props:{},
  data(){
    return{
    }
  },
  computed:{
    ...mapGetters([
        'PRODUCTS',
        'CART',
        'PROFILE'

    ]),
  },
  methods:{
    ...mapActions([
        'GET_PRODUCT_FROM_API',
        'ADD_TO_CART'
    ]),
    addToCart(data){
      this.ADD_TO_CART(data);
    }
  },
  mounted() {
    this.GET_PRODUCT_FROM_API()
    .then((response)=>{
      if (response.data){
        console.log('Data received')
      }
    })
  }
}
</script>

<style>
 .v-catalog {
   display: flex;
   flex-wrap: wrap;
   justify-content: center;
   text-align: center;

 }
 .v-catalog__link_to_cart{
   position: absolute;
   top:10px;
   right: 10px;
   padding: 16px;
   border: solid 1px green;
   margin: 10px;
   cursor: pointer;
   font-size: 20px;
 }
 .v-catalog__link_to_profile{
   position: absolute;
   top:10px;
   right: 200px;
   padding: 16px;
   border: solid 1px green;
   margin: 10px;
   cursor: pointer;
   font-size: 20px;
 }
 .v-catalog__header{
   position: absolute;
   top:10px;
   left: 10px;
   padding: -11px;
   margin: 10px;
   font-size: 50px;
 }


</style>