/* eslint-disable no-new */
<template>
<div class="home">
  <div class="container">
    <div class="row mt-4">

      <div v-for="product in products" :key="product.id" class="col-md-4 col-lg-3 col-sm-6">
        <div class="card my-2">
          <div class="img-contain">
            <img :src="product.image" class="card-img-top" alt="...">
          </div>
          <div class="card-body">
            <h5 class="card-title text-capitalize mb-1">{{product.name}}</h5>
            <p class="mt-1 price">#{{product.price.toLocaleString()}} <sup class="text-danger"><strike>#{{product.discount.toLocaleString()}}</strike></sup> </p>
            <button :disabled="inCart.includes(product.id)" @click="addCartItem(product.id)" class="btn btn-success btn-sm"><i :class="inCart.includes(product.id) === true ? '' : 'fa fa-plus' "></i> {{inCart.includes(product.id) === true ? 'Added' : 'Add To Cart'}}</button>
          </div>
        </div>
      </div>

    </div>
  </div>
</div>
</template>

<script>
import { mapActions, mapState } from 'vuex'

export default {
  name: 'Home',
  computed: {
    ...mapState({
      products: state => state.products.forSale,
      inCart: state => state.products.cartItems
    })
  },
  methods: {
    ...mapActions({
      addToCart: 'products/addToCart'
    }),
    addCartItem (id) {
      this.addToCart(id)
    }
  }
}
</script>

<style scoped>
  .img-contain{
    width: 100%;
    height: 210px;
  }
  .img-contain img{
    width: 100%;
    height: 100%;
  }
  .price{
    font-weight: 200;
  }
</style>
