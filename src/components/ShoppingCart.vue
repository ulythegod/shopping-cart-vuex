<template>
    <div>
        <h1>Shopping list</h1>
        <ul>
            <li v-for="(product, index) in products" :key="index">
                {{ product.title }} - {{ product.price | currency}} - {{ product.quantity }}
            </li>
        </ul>
        <p>Total: {{ total | currency}}</p>
        <button @click="checkout">Checkout</button>
        <p>Checkout status: {{ checkoutStatus }}</p>
    </div>
</template>

<script>
import store from '../store/index';

export default {
    computed: {
        products () {
            return store.getters.cartProducts
        },
        total () {
            return store.getters.cartTotal
        },
        checkoutStatus () {
            return store.getters.checkoutStatus
        }
    },
    methods: {
        checkout () {
            store.dispatch('checkout')
        }
    }
}
</script>


<style scoped>

</style>
