<template>
  <div class="v-cart-item">
    <img class="v-cart-item__image" :src="imgLink" :alt="cart_item_data.name" />
    <div class="v-cart-item__info">
      <p>{{cart_item_data.name}}</p>
      <p style="color: green">{{cart_item_data.price}}$</p>
      <p>{{cart_item_data.article}}</p>
    </div>
    <div class="v-cart-item__quantity">
      <p>Quantity:</p>
      <span>
        <span class="quantity__btn" @click="decrementItem">-</span>
              {{cart_item_data.quantity}}
        <span class="quantity__btn" @click="incrementItem">+</span>
      </span>
    </div>
    <button class="v-catalog-item__delete_from_cart_btn" @click="deleteFromCart">Delete</button>
  </div>
</template>

<script>

export default {
  name: "v-cart-item",
  props:{
    cart_item_data:{
      type: Object,
      default(){
        return{}
      }
    }
  },
  data(){
    return {}
  },
  computed: {
    imgLink: function () {
      const fileName = this.cart_item_data.image;
      return require(`../assets/images/${fileName}`);
    }
  },
  methods:{
    decrementItem(){
      this.$emit('decrement')

    },
    incrementItem(){
      this.$emit('increment')
    },
    deleteFromCart(){
      this.$emit('deleteFromCart')
    }
  },
  mounted() {
  }
}

</script>

<style>
  .v-cart-item{
    display: flex;
    flex-wrap: nowrap;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 0 8px 0 #e0e0e0;
    padding: 16px;
    margin-bottom: 16px;
  }
  .v-cart-item__image{
    max-width: 50px;
  }
  .v-catalog-item__delete_from_cart_btn{
    border-radius: 8px;
    color: black;
    border: 1px solid green;
    background: white;
    font-size: 20px;
    font-family: Constantia;
  }
  .quantity__btn{
    cursor: pointer;
  }
</style>