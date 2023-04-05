<template>
    <div>
        <h1>Product list</h1>
        <img
            v-if="loading"
            src="https://i.imgur.com/JfPpwOA.gif"
        >
        <ul v-else>
            <li v-for="(product, index) in allProducts" :key="index">
                {{ product.title }} - {{ product.price | currency }} - {{ product.inventory }}
                <button 
                    @click="addProductToCart(product)" 
                    :disabled="!productIsInStock(product)"
                >
                    Add to cart
                </button>
            </li>
        </ul>
    </div>
</template>

<script>
import store from '../store/index';

export default {
    data () {
        return {
            loading: false
        }
    },
    computed: {
        products () {
            return store.getters.availableProducts
        },
        productIsInStock () {
            return store.getters.productIsInStock
        }
    },
    methods: {
        addProductToCart(product) {
            store.dispatch('addProductToCart', product);
        }
    },
    created() {
        this.loading = true
        store.dispatch('fetchProducts').then(() => {
            this.loading = false
        })
    }, 
}
</script>

<style scoped>
</style>