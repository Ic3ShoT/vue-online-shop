<template>

  <div class="v-catalog-item">
    <v-popup
      v-if="isInfoPopupVisible"
      rightBtnTitle="Add to cart"
      :popupTitle="product_data.name"
      @closePopup="closeInfoPopup"
      @rightBtnAction="addToCart"

    >

      <div>
        <p class="v-popup__info">{{product_data.info}}</p>
      </div>
    </v-popup>


    <img :src="imgLink" :alt="product_data.name" />
    <p class="v-catalog-item__name">{{product_data.name}}</p>
    <p class="v-catalog-item__artist">{{product_data.artist}}</p>
    <p class="v-catalog-item__catalog">Catalog: {{product_data.catalog}}</p>
    <p class="v-catalog-item__price">{{product_data.price}}$</p>
    <button
        class="v-catalog-view_info"
        @click="showPopupInfo"
    >Show info</button>
    <button
        class="v-catalog-item__add_to_cart_btn btn"
        @click="addToCart">
      Add to cart
    </button>
  </div>
</template>

<script>
import vPopup from '../components/popup/v-popup'
export default {
  name: "v-catalog-item",
  components:{
    vPopup
  },
  props:{
    product_data: {
      type: Object,
      default(){
        return{}
      }
    }
  },
  data(){
    return{
      isInfoPopupVisible: false
    }
  },
  computed: {
    imgLink: function () {
      const fileName = this.product_data.image;
      return require(`../assets/images/${fileName}`);
    },

  },
  methods:{
    showPopupInfo(){
      this.isInfoPopupVisible = true;
    },
    closeInfoPopup(){
      this.isInfoPopupVisible = false;

    },
    addToCart(){
      this.$emit('addToCart',this.product_data);
    }
  },
  mounted() {
    this.$set(this.product_data,'quantity',1)

  }


}
</script>

<style>
.v-catalog-item{
  box-shadow: 0 0 8px 0 slategray;
  padding: 16px;
  margin-bottom: 16px;
  border-radius: 30px;

}

.v-catalog-item__artist{
  font-size: 22px;
  font-style: initial;
  font-family: "Roboto Thin";
}
.v-catalog-item__name{
  font-size: 30px;
  font-family: Constantia;
}
.v-catalog-item__price{
  color: green;
  font-size: 19px;
  font-family: "Droid Sans Mono";
  font-style: italic;
}
.v-catalog-item__catalog{
  font-size: 20px;
  font-family: Gabriola;
}
.v-catalog-item__add_to_cart_btn{
  border-radius: 8px;
  color: black;
  border: 1px solid green;
  background: white;
  font-size: 20px;
  font-family: Constantia;
  cursor: pointer;
}
.v-catalog-view_info{
  border-radius: 8px;
  color: black;
  border: 1px solid green;
  background: white;
  font-size: 20px;
  font-family: Constantia;
  background: #26ae68 ;
  cursor: pointer;
}
.v-popup__info{
  font-family: Arial;
  font-size: 20px;
  cursor: pointer;
}
</style>