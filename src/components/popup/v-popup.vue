<template>
  <div class="v-popup">
    <div class="v-popup__header">
      <span style="font-style: italic">{{ popupTitle }}</span>
      <span>
        <i
            @click="closePopup"
            class="material-icons">close</i>
      </span>
    </div>
    <div class="v-popup__content">
      <slot></slot>
    </div>
    <div class="v-popup__footer">
      <button class="close_modal" @click="closePopup">Close</button>
      <button
          class="submit_btn"
          @click="rightBtnAction"
      >{{rightBtnTitle}}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "v-popup",
  props:{
    popupTitle:{
      type: String,
      default: 'Popup name'
    },
    rightBtnTitle: {
      type: String,
      default: 'Ok'
    }
  },
  data(){
    return{}
  },
  methods:{
    rightBtnAction(){
      this.$emit('rightBtnAction')
    },
    closePopup(){
      this.$emit('closePopup')
    }
  },
  mounted() {

  }
}
</script>

<style>
 .v-popup{
   padding: 16px;
   position: fixed;
   top: 50px;
   left: 735px;
   width: 400px;
   background: white;
   box-shadow: 0 0 17px #e7e7e7;
   z-index: 10;
   max-width: 600px;
   border-radius: 8px;
 }
  .v-popup__header{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .v-popup__content{
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .v-popup__footer{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .submit_btn{
    padding: 8px;
    color: white;
    background: #26ae68;
    cursor: pointer;
  }
  .close_modal{
    padding: 8px;
    color: white;
    background: red;
    cursor: pointer;
  }
</style>