<template>
  <div class="v-cart">
    <router-link :to="{name: 'catalog'}">
      <div class="v-catalog__link_to_cart">Back to Catalog</div>
    </router-link>
    <router-link :to="{name: 'profile', params: {cart_data: CART}}">
      <div class="v-catalog__link_to_profile">
        Profile
      </div>
    </router-link>
    <h1 style="font-size: 50px">Cart:</h1>
    <p v-if="!cart_data.length">Cart is empty...</p>
    <v-cart-item
      v-for="(item,index) in cart_data"
      :key="item.article"
      :cart_item_data="item"
      @deleteFromCart="deleteFromCart(index)"
      @increment="increment(index)"
      @decrement="decrement(index)"
    />
    <div class="v-cart__total">
      <p class="total__name">Total:</p>
      <p>{{cartTotalCost}}$</p>
    </div>
  </div>
</template>

<script>
import vCartItem from './v-cart-item'
import {mapActions} from "vuex"

export default {
  name: "v-cart",
  components:{
    vCartItem
  },
  props:{
    cart_data:{
      type: Array,
      default() {
        return [ ];
      }
    }
  },
  data(){
    return{}
  },
  computed:{
    cartTotalCost(){
      let result = []
      if (this.cart_data.length){
        for (let item of this.cart_data){
          result.push(item.price * item.quantity) ;
        }
        result = result.reduce(function (sum,el){
          return sum + el;
        })
        return result;
      } else{
        return 0
      }


    }
  },
  methods:{
    ...mapActions([
        'DELETE_FROM_CART',
      'INCREMENT_CART_ITEM',
      'DECREMENT_CART_ITEM'
    ]),
    increment(index){
      this.INCREMENT_CART_ITEM(index)
    },
    decrement(index){
      this.DECREMENT_CART_ITEM(index)
    },
    deleteFromCart(index){
      this.DELETE_FROM_CART(index)
    }
  }
}
</script>

<style>
 .v-cart{
   text-align: center;
   margin-bottom: 100px;
 }
 .v-cart__total{
   position: fixed;
   bottom: 0;
   right: 0;
   left: 0;
   padding: 16px 24px;
   display: flex;
   justify-content: center;
   background: #003d00;
   color: white;
   font-size: 20px;
 }
 .total__name{
   margin-right: 16px;
 }

</style>