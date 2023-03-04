<template>
    <div class="container">
        <h1 class="heading">Các sản phẩm nổi bật</h1>
        <div class="product-list">
            <ProductItem v-for="productItem in productList" :key="productItem.id" :productItem="productItem"></ProductItem>
        </div>
    </div>
</template>

<script>
import store from '@/store';
import ProductItem from './ProductItem.vue';
export default {
    data() {
        return {
            productList: store.productList
        }
    },
    components: { ProductItem }
}
</script>

<style scoped>
.container {
    padding: 20px;
    width: 1280px;
    max-width: 100%;
    margin: 0 auto;
}

.heading {
    color: red;
    text-align: center;
}

.product-list {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    column-gap: 30px;
    row-gap: 30px;
}
</style>