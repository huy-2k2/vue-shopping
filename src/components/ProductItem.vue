<template>
    <div class="product">
        <img class="product-image" :src="imageUrl" alt="">
        <div class="product-container">
            <h3 class="product-name">{{ productItem.name }}</h3>
            <div class="product-price">{{ priceFormated }} Vnđ</div>
            <div class="product-option">
                <button @click="handleAddToCart(productItem.id)" class="product-button product-button--buy">Mua</button>
                <button @click="handleOpenModal" class="product-button product-button--detail">Chi tiết</button>
            </div>
        </div>
        <Teleport v-if="isopenModal" to="#app">
            <TheModal :handleCloseModal="handleCloseModal">
                <div class="product-detail">
                    <div class="product-detail-image">
                        <img :src="imageUrl" alt="">
                    </div>
                    <div class="product-detail-content">
                        <div class="product-detail-item">
                            <span class="product-detail-title">Name:</span>
                            <span class="product-detail-text">{{ productItem.name }}</span>
                        </div>
                        <div class="product-detail-item">
                            <span class="product-detail-title">Description:</span>
                            <span class="product-detail-text">{{ productItem.description }}</span>
                        </div>
                        <div class="product-detail-item">
                            <span class="product-detail-title">Price:</span>
                            <span class="product-detail-text">{{ priceFormated }} Vnđ</span>
                        </div>
                    </div>
                </div>
            </TheModal>
        </Teleport>
    </div>
</template>

<style scoped>
.product-detail-content {
    display: flex;
    flex-direction: column;
    row-gap: 10px;
}

.product-detail-item {
    padding: 10px 20px;
    border-radius: 10px;
    background-color: rgba(106, 153, 106, 0.527);
}

.product-detail-title {
    font-size: medium;
    font-weight: bold;
}

.product-detail {
    display: flex;
    align-items: start;
    justify-content: start;
    column-gap: 20px;
}

.product-detail-image {
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 10px;
    width: 200px;
    flex-shrink: 0;
}

.product-detail-image img {
    max-width: 100%;
}

.product {
    border-radius: 4px;
    border: 1px solid #ccc;
}

.product-image {
    width: 100%;
}

.product-container {
    padding: 8px 20px;
}

.product-price {
    margin: 12px 0;
    color: red;
}

.product-option {
    display: flex;
    align-items: center;
    justify-content: start;
    column-gap: 8px;
}

.product-button {
    padding: 8px 12px;
    border-radius: 4px;
    border: none;
    font-weight: bold;
    color: white;
    cursor: pointer;
}

.product-button--buy {
    background-color: red;
}

.product-button--detail {
    background-color: rgb(9, 139, 183);
}
</style>

<script>
import store from '@/store';
import TheModal from './TheModal.vue';
export default {
    data() {
        return {
            isopenModal: false
        }
    },
    components: { TheModal },
    props: {
        productItem: {
            type: Object,
            required: true
        }
    },
    computed: {
        imageUrl() {
            return `/images/${this.productItem.image}.webp`
        },
        priceFormated() {
            return this.productItem.price.toLocaleString('it-IT', { style: 'currency', currency: 'VND' })
        },
    },
    methods: {
        handleAddToCart(productId) {
            const cartItem = store.cartList.find((item) => item.productId == productId)
            if (cartItem) {
                if (cartItem.quantity < store.productList.filter(product => product.id == cartItem.productId)[0].quantityInStock)
                    cartItem.quantity++
            }
            else
                store.cartList.unshift({ productId, quantity: 1 })
        },
        handleOpenModal() {
            this.isopenModal = true
        },
        handleCloseModal() {
            this.isopenModal = false
        }
    }

}
</script>

