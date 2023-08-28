<template>
    <div class="product-list">
        <div>
            <h1>Product List</h1>
            <button @click="clearList">Clear list</button>
        </div>

        <div class="adding-form">
            <input type="text" v-model="newProductName">
            <button @click="addNewProduct">Add product</button>
        </div>

        <ul class="product-list">
            <li v-for="(product, index) in productList" :key= "index">
                <ProductItem @crossOut="handleCrossOut(index)" :name="product.name" :isCrossedOut = "product.isCrossedOut" />
            </li>
        </ul>
    </div>
</template>

<script>
import ProductItem from './ProductItem.vue'

export default {
    name: 'ProductList',
    components: {
        ProductItem
    },
    data() {
        return {
            productList: [],
            newProductName: ''
        }
    },

    mounted() {
        const savedList = localStorage.getItem('product-list');
        if (savedList) {
            this.productList = JSON.parse(savedList)
        }
    },

    watch: {
        productList: {
            handler() {
                localStorage.setItem('product-list', JSON.stringify(this.productList))
            },
            deep: true,
        }
    },

    methods: {
        addNewProduct() {
            if( this.newProductName !== '') {
                this.productList.push({name: this.newProductName, isCrossedOut: false});
                this.newProductName = '';
                return;
            }
        },

        clearList() {
            localStorage.removeItem('product-list');
            this.productList = [];
        },

        handleCrossOut(index) {
            let product = this.productList[index];

            if (product.isCrossedOut === false) {
                product.isCrossedOut = true;
                this.productList.splice(index, 1);
                this.productList.push(product);
                return;
            }

        }
    }

}

</script>

<style>
 li {
    list-style: none;
 }

 .adding-form {
    margin-top: 20px;
    display: flex;
    justify-content: center;
    gap: 10px;
 }

 .product-list {
    display: flex;
    flex-direction: column;
    gap: 10px;
 }
</style>