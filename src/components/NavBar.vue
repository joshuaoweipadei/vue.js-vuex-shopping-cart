/* eslint-disable no-new */
<template>
<div id="app">
    <div id="nav">
        <nav class="navbar navbar-expand-md navbar-light" style="background-color: #e3f2fd;">
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarText" aria-controls="navbarText" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <button class="btn btn-primary btn-sm btn-cart-1" data-toggle="modal" data-target="#shoppingCart"><i class="fa fa-shopping-cart"></i> Cart<sup>{{inCart.length}}</sup></button>
            <div class="collapse navbar-collapse" id="navbarText">
                <a class="navbar-brand" href="#">ShoppingCart</a>
                <ul class="navbar-nav mr-auto">
                    <li class="nav-item">
                        <router-link to="/" class="nav-link">Home </router-link>
                    </li>
                    <li class="nav-item">
                        <router-link to="/about" class="nav-link">About</router-link>
                    </li>
                </ul>
                <span class="navbar-text">
                    <button class="btn btn-primary btn-sm btn-cart-2" data-toggle="modal" data-target="#shoppingCart"><i class="fa fa-shopping-cart"></i> Cart<sup>{{inCart.length}}</sup></button>
                </span>
            </div>
        </nav>

        <div id="shoppingCart" class="modal fade">
          <div class="modal-dialog">
            <div class="modal-content">
              <div class="modal-header">
                <h5 class="modal-title">ShoppingCart</h5>
                <button class="close" data-dismiss="modal">
                  &times;
                </button>
              </div>
              <div class="modal-body">

                <table v-if="cartItems.length > 0" class="table table-bordered table-responsive">
                  <thead style="background-color: #e3f2fd;">
                    <th width="5%"></th>
                    <th colspan="2">Product Name</th>
                    <th width="18%" class="text-center">Qty</th>
                    <th width="7%" class="text-center">Price(#)</th>
                  </thead>
                  <tbody>
                    <tr v-for="(cartItem, index) in cartItems" :key="index" >
                      <td class="text-center">
                        <button class="btn btn-outline-danger btn-sm" @click="remove(index)"><i class="fa fa-close"></i></button>
                      </td>
                      <td class="text-capitalize">{{ cartItem.name }}</td>
                      <td class="">
                        <div style="width:50px; height:50px">
                          <img :src="cartItem.image" :alt="cartItem.image" width="100%" height="100%">
                        </div>
                      </td>
                      <td>
                        <input type="number" min="1" max="9" class="form-control" v-model="cartItem.qty" style="width:55px">
                      </td>
                      <td>{{ (cartItem.qty * cartItem.price).toLocaleString() }}</td>
                    </tr>
                    <tr>
                      <td colspan="2" class="border-right-0"><b>Total:</b></td>
                      <td colspan="3" class="text-right border-left-0"><b>{{total.toLocaleString()}}</b></td>
                    </tr>
                  </tbody>
                </table>

                <div v-else class="text-center">You have no item in cart</div>

              </div>
              <div class="modal-footer">
                <button class="btn btn-secondary btn-sm" data-dismiss="modal">Keep shopping</button>
                <button :disabled="cartItems.length < 1" class="btn btn-primary btn-sm" @click="checkOut(cartItems)"><i class="fa fa-shopping-cart"></i> Check out</button>
              </div>
            </div>
          </div>
        </div>
    </div>
</div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
  created () {
    console.log(this.$router.currentRoute.meta)
  },
  computed: {
    ...mapState({
      inCart: state => state.products.cartItems,
      cartItems: state => state.products.cartItems.map((cartItem) => {
        return state.products.forSale.find((forSaleItem) => {
          return cartItem === forSaleItem.id
        })
      })
    }),
    total () {
      return this.cartItems.reduce((acc, cur) => acc + (cur.qty * cur.price), 0)
    }
  },
  methods: {
    ...mapActions({
      removeCartItem: 'products/removeCartItem',
      updateCart: 'products/updateCart'
    }),
    remove (id) {
      this.removeCartItem(id)
    },
    checkOut (data) {
      alert('I\'ll be building the backend for this app with Node.js and MongoDB soon 😃 🤖 🚀 ')
      // console.log(data)
    }
  }
}
</script>

<style scoped>
  th{
    border-top: 0px
  }
  sup{
    font-weight: 600;
  }
  @media screen and (min-width: 768px) {
    .btn-cart-1{
      display: none;
    }
  }
  @media screen and (max-width: 767px) {
    .btn-cart-2{
      display: none;
    }
  }
</style>
