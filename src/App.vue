<template>
  <div id="app">
    <theHeader :cart="cart" @cartUpdate="cartUpdate" class="bg-white"/>
      <b-container>
        <b-row>
          <productList v-for="(item, i) in productObject" :key="i" :product="item" @addProduct="addCart" />
        </b-row>
      </b-container>
  </div>
</template>

<script>
import theHeader from './components/theHeader.vue'
import productList from './components/productList.vue'

export default {
  name: 'App',
  components: {
    theHeader,
    productList
  },
	data () {
		return{
			productObject: [ // Product List
				{ id:0, title: 'Zoom Freak 3', rating: 4, colors: [
          require("@/assets/products-img/zoom-freak.jpg"),
          require("@/assets/products-img/zoom-freak-2.jpg"),
          require("@/assets/products-img/zoom-freak-3.jpg"),
          require("@/assets/products-img/zoom-freak-4.jpg")
          ], prices: [33,35,36,37,39],size: [34,36,38,40,42] },

				{ id:1, title: 'Kyrie Low', rating: 5, colors: [
          require("@/assets/products-img/kyrie-low.jpg"),
          require("@/assets/products-img/kyrie-low-2.jpg"),
          require("@/assets/products-img/kyrie-low-3.jpg"),
          require("@/assets/products-img/kyrie-low-4.jpg")
          ], prices: [48,53,54,55,57],size: [34,36,38,40,42] },
				{ id:2, title: 'Giannis', rating: 3, colors: [
          require("@/assets/products-img/giannis-immortality.jpg"),
          require("@/assets/products-img/giannis-immortality-2.jpg"),
          require("@/assets/products-img/giannis-immortality-3.jpg"),
          require("@/assets/products-img/giannis-immortality-4.jpg")
          ], prices: [66,67,69,70,72],size: [34,36,38,40,42] },

				{ id:3, title: 'Lebron Witness', rating: 4, colors: [
          require("@/assets/products-img/lebron-witness.jpg"),
          require("@/assets/products-img/lebron-witness-2.jpg"),
          require("@/assets/products-img/lebron-witness-3.jpg"),
          require("@/assets/products-img/lebron-witness-4.jpg")
          ], prices: [80,84,85,86,88],size: [34,36,38,40,42] },
			],
			cart: []
		}
	},
	methods: {
    addCart(val) { //Add the incoming product to the cart.
       let control = this.cart.find(l=> 
       l.id == val.id && 
       l.color == val.color && 
       l.size == val.size);
      if(!control){ this.cart.push(val); }else{ control.count = control.count + val.count; }
    },
    cartUpdate(cart) { //Let's update the changed cart from the header component.
      this.cart = cart;
    },
	}
}
</script>

<style>

html, 
body {
    margin: 0;
    padding: 0;
    background-color: rgb(230, 230, 230) !important;
}
</style>
