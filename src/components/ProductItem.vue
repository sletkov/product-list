<template>
    <div class="product-item">
        <h2 :class="{crossedOut: isCrossedOut}">{{ name }}</h2>
        <button class="btn" @click="crossOutProduct">Cross out</button>
    </div>
</template>

<script>

export default {
    name: 'ProductItem',
    props: {
      name: String,
      isCrossedOut: Boolean
    },
    methods: {
        crossOutProduct() {
            this.$emit('crossOut')
        }
    }
}

</script>

<style>
    .product-item {
        display: flex;
        border-radius: 20px;
        justify-content: space-between;
        align-items: center;
        border: 1px solid black;
        padding: 5px 15px;
    }

    .crossedOut {
        text-decoration: line-through;
    }

    .btn {
        height: 30px;
    }
</style>