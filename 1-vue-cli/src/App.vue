<!--Its like a root component. 
The component that will be displayed in the template must have been imported in here and used on the template, also we should enter the component in the components property. 
We can assign a special name for the component we use but the component's original name must be given as the value for the special name.-->

<template>
  <div class="container">
    <!-- <MyComp /> -->
    <div class="cart">
      <h3>Cart</h3>
      <ul>
        <li v-for="item in cartItems" :key="item.id">{{ item.title }}</li>
      </ul>
      <p v-if="cartItems.length == 0">Your cart is empty. Start shopping now!</p>
    </div>

    <Product
      @addToCart="cartItems.push($event)"
      :product="product"
      v-for="product in productList"
      :key="product.id"
    />
  </div>
</template>

<script>
// import MainContainer from "@/ components/MainContainer"
import Product from "@/components/Product";

export default {
  components: {
    // MyComp : MainContainer,
    Product,
  },
  data() {
    return {
      productList: [
        {
          id: 1,
          title: "MacBook Pro",
          description: "Macbook Pro for you",
          price: 7000,
          count: 30,
        },
        {
          id: 2,
          title: "Bluetooth Mouse",
          description: "Bluetooth mouse for you",
          price: 75,
          count: 265,
        },
        {
          id: 3,
          title: "Keyboard",
          description: "Keyboard for you",
          price: 100,
          count: 150,
        },
      ],
      cartItems: [],
    };
  },
};
</script>

<style>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.cart{
  margin-bottom: 50px;
}
</style>
