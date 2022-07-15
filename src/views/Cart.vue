<template>
  <div class="w-full h-full px-3 lg:px-0 lg:w-4/5 mx-auto mt-20 mb-20 cart-cart ">
    <div class="lg:flex lg:items-center mb-14">
    <h1 class="font-semibold my-3 mr-20">Cart</h1>
    <p class="hover:text-prpl transition"><router-link to="/products">Back</router-link></p>
    </div>
    <div v-for="(p, index) in cart" :key="p.id">
      <div class="flex my-20">
      <div class="w-3/12 bg-neutral-100 rounded-lg p-10 border-b border-lghtprpl">
        <img class="w-full rounded-lg mb-10" :src="'http://38.242.229.113:8055/assets/' + p.image.id" alt="">
        <p class="font-semibold mb-2">{{ p.title }}</p>
        <p>Price: <span class="text-prpl">{{ p.price }}</span></p>
      </div>  
      <button @click="deleteFromCartLocal(index)" class="mt-52 ml-40 w-40 h-14 text-prpl bg-neutral-100 hover:bg-black/10 rounded-lg transition">
        Delete from cart
      </button>
      </div>
      </div>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity';
import { deleteFromCart } from '../utils/cart'
export default {
  setup() {
    let cart = ref(JSON.parse(sessionStorage.getItem('cart')));
    const deleteFromCartLocal = (index) => {
      cart.value.splice(index,1)
      deleteFromCart(index)
    }
    return {
      cart,
      deleteFromCart,
      deleteFromCartLocal
    }
  },
};
</script>
