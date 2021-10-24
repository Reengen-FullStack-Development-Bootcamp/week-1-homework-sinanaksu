<template>
          <div class="col-sm-3">
            <div class="card">
            <img :src="product.colors[sColor]" class="card-img-top" width="100%">
                <div class="card-body pt-0 px-0" >
                    <div class="d-flex flex-row justify-content-between mb-3 px-0" >
                        <img v-for="(src,index) in product.colors" :key="index" :src="src" :class="index==sColor?'selected-img':''" role="button" @click="sColor=index" width="25%">
                    </div>

                    <div class="d-flex flex-row justify-content-between mb-0 px-3">
                    <span class="fw-bold">{{product.title}}</span>
                      <small>
                      <span v-for="(el,i) in product.rating" :key="i" class="fa fa-star checked" />
                      <span v-for="(el,i) in (5 - product.rating)" :key="'empty-'+i" class="fa fa-star" />
                      </small>
                    </div>
                    <hr class="mt-2 mx-3">
                    <div class="d-flex flex-row justify-content-between px-3 pb-4">
                        <div class="d-flex flex-column">PRICE</div>
                        <div class="d-flex flex-column">
                            <h4 class="mb-0">$ {{ product.prices[sSize] }}</h4>
                        </div>
                    </div>
                    <div class="d-flex flex-row justify-content-center ">
                      <b-row>
                        <b-col>Size</b-col>
                        <b-col>
                          <nav>
                          <ul class="pagination">
                          <li v-for="(size,index) in product.size" :key="index"  class="page-item"><a class="page-link" :class="index==sSize?'selected-size':''" href="#" @click="sSize=index" >{{size}}</a></li>
                          </ul>
                          </nav>              
                        </b-col>
                      </b-row>
                    </div>
                    
                    <div class="mx-3 mt-3 mb-0"><button type="button" class="btn btn-light btn-block" @click="addCart"><small>ADD CART</small></button></div>
                </div>
            </div>
        </div>
</template>

<script>
export default {
  name: 'productList',
	props: {
		product: Object
	},
	data() { //Let's define the necessary variables
		return {
      sSize: 0,
      sPrice: 0,
      sCount: 1,
      sColor: 0,
      sId: this.product.id
		}
	},
	methods: {
		addCart() { //Add the selected product to the cart
			this.$emit('addProduct', {id:this.sId,size:this.sSize,price:this.product.prices[this.sSize],count:this.sCount,color:this.sColor,img:this.product.colors[this.sColor]});
		},
	}
}
</script>

<style>

.page-link {
    padding: 0.2rem 0.4rem !important;
    border: 1px solid grey;
    color: grey !important;
}

.selected-size {
    color: black !important;
    background-color: #ccc !important;
}

.selected-img {
    border-bottom:3px solid orange;
}

.card {
    border-radius: 20px !important;
    border-color: rgba(153, 153, 153, 0.7) !important;
}

.card:hover {
    -webkit-box-shadow: 0 4px 15px rgba(153, 153, 153, 0.7);
    box-shadow: 0 4px 15px rgba(153, 153, 153, 0.7);
    -webkit-transition: .3s;
    transition: .3s
}

.card-img-top {
    border-top-right-radius: 20px !important;
    border-top-left-radius: 20px !important;
    border-bottom:1px solid #ccc;
}

span.text-muted {
    font-size: 12px
}

small.text-muted {
    font-size: 8px
}

h5.mb-0 {
    font-size: 1rem
}

small.ghj {
    font-size: 9px
}

.mid {
    background: #ECEDF1
}

h6.ml-1 {
    font-size: 13px
}

.btn-light {
  width:100%;
  border-radius: 10px !important;
  border:1px solid #ccc !important;
}

.btn-light:focus {
    box-shadow: none
}

@media screen and (max-width:600px) {
    .col-sm-3 {
        margin-bottom: 50px
    }
}
.checked {
	color: orange;
}

.vibration:hover {
  animation: shake 0.82s cubic-bezier(.36,.07,.19,.97) both;
  transform: translate3d(0, 0, 0);
  backface-visibility: hidden;
  perspective: 1000px;
}

@keyframes shake {
  10%, 90% {
    transform: translate3d(-1px, 0, 0);
  }
  
  20%, 80% {
    transform: translate3d(2px, 0, 0);
  }

  30%, 50%, 70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%, 60% {
    transform: translate3d(4px, 0, 0);
  }
}

</style>
