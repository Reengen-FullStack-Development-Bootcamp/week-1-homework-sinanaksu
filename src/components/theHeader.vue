<template>
<div>
<b-container>
  <b-row>
    <b-col><img alt="Fake" src="../assets/logo.png" /></b-col>
    <b-col></b-col>
    <b-col class="text-end"><span  class="me-3 fw-bold">Register</span> <span class="ms-3 fw-bold">Sign In</span></b-col>
  </b-row>
</b-container>


  <b-navbar type="dark" variant="dark" class="bg-black text-white d-flex mb-5">
    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
    <b-container >
      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav class="me-auto">
          <b-nav-item href="#">Men</b-nav-item>
          <b-nav-item href="#">Women</b-nav-item>
          <b-nav-item href="#">Kids</b-nav-item>
        </b-navbar-nav>
        <b-navbar-nav class="d-flex">
          <b-nav-item-dropdown class="cartStyle">
              <template #button-content>
                <i class="fas fa-shopping-cart"></i> {{ cartCount }}
              </template>
              
              <b-row v-for="(line,index) in cart" :key="index" >
              <b-col><img :src="line.img" height="30"/></b-col>
              <b-col>${{ line.price}} x {{ line.count}}</b-col>
              <b-col>
                <b-button-group size="sm">
                  <b-button variant="success" @click="positive(index)"> + </b-button>
                  <b-button variant="primary" @click="negative(index)"> - </b-button>
                  <b-button variant="danger" @click="deleted(index)"> x </b-button>
                </b-button-group>
              </b-col> 
              </b-row>
          </b-nav-item-dropdown>
        </b-navbar-nav>

      </b-collapse>
    </b-container>
  </b-navbar>
  
</div>
</template>

<script>
export default {
  name: 'theHeader',
  props: {
    cart: Array,
  },
  computed: {
		cartCount() {//Let's update the cart detail and total.
      console.log(this.cart);
			let count = 0
      let price = 0
			for (let i = 0; i < this.cart.length; i++) {
				count += this.cart[i].count
        price += this.cart[i].price * this.cart[i].count
			}
			return "$" + price + " for " + count + " Product"
		}
	},
  methods: {
    deleted(i){ //Let's delete the product from the cart.
      this.cart.splice(i,1)
    },
    negative(i){//Let's reduce the product from the cart.
      if(this.cart[i].count == 1) {
        this.deleted(i);
      } else {
        this.cart[i].count = this.cart[i].count - 1;
      }
    },
    positive(i){//Let's increase the product from the cart.
        this.cart[i].count = this.cart[i].count + 1;
    }
  }
}
</script>

<style >
.navbar {
  box-shadow: 0 0.5rem 1rem rgb(0 0 0 / 45%), inset 0 -1px 0 rgb(0 0 0 / 15%);
}
.cartStyle{
  background-color:#fff;
  border-radius:5px;
  color:#000 !important;
  min-width:300px !important;
  text-align:center;
}
.cartStyle a {
    color:#000 !important;
    min-width:300px !important;
}
</style>
