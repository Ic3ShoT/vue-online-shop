<template>
  <div class="v-profile">
    <router-link :to="{name: 'catalog'}">
      <div class="v-catalog__link_to_cart">Back to Catalog</div>
    </router-link>
    <h1>Profile</h1>
    <form>
      <label for="fname">First name:</label><br>
      <input type="text" id="fname" name="fname" value="Brian"><br>
      <label for="lname">Last name:</label><br>
      <input type="text" id="lname" name="lname" value="Molko"><br>
      <label for="fname">Email:</label><br>
      <input type="text" id="email" name="email" value="brianmolko@gmail.com"><br>
      <label for="lname">Phone number:</label><br>
      <input type="text" id="age" name="age" value="+44 203 411 7482"><br><br>
      <input type="submit" class="v-catalog-item__add_to_cart_btn btn" value="Submit">
    </form>
  </div>
</template>

<script>
export default {
  name: "v-profile"
}
</script>

<style>
.v-profile{
  text-align: center;
  font-family: Calibri;
}

</style>