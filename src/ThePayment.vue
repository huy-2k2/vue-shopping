<template>
    <table style="width:400px">
        <tr>
            <th>STT</th>
            <th>Tên</th>
            <th>Giá</th>
            <th>Số lượng trong kho</th>
            <th>Số lượng</th>
            <th>Thành tiền</th>
            <th>Hàng động</th>
        </tr>
        <tr v-for="(cartItem, index) in store.cartList" :key="cartItem.productId">
            <td>{{ index + 1 }}</td>
            <td>{{ getProduct(cartItem.productId).name }}</td>
            <td>{{ formatPrice(getProduct(cartItem.productId).price) }} vnd</td>
            <td>{{ getProduct(cartItem.productId).quantityInStock }}</td>
            <td>
                <span @click="handleIncrement(cartItem.productId)">tang</span>
                {{ cartItem.quantity }}
                <span @click="handleDecrement(cartItem.productId)">giam</span>
            </td>
            <td>{{ formatPrice(cartItem.quantity * getProduct(cartItem.productId).price) }}</td>
            <td @click="handleRemove(cartItem.productId)">
                <svg xmlns="http://www.w3.org/2000/svg" class="ionicon" viewBox="0 0 512 512">
                    <title>Trash Bin</title>
                    <path d="M432 144l-28.67 275.74A32 32 0 01371.55 448H140.46a32 32 0 01-31.78-28.26L80 144" fill="none"
                        stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="32" />
                    <rect x="32" y="64" width="448" height="80" rx="16" ry="16" fill="none" stroke="currentColor"
                        stroke-linecap="round" stroke-linejoin="round" stroke-width="32" />
                    <path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="32"
                        d="M312 240L200 352M312 352L200 240" />
                </svg>
            </td>
        </tr>
    </table>
    <p>total: {{ totalCost }}</p>
</template>

<script>
import store from './store';
export default {
    computed: {
        store() {
            const { productList, cartList } = store
            return { productList, cartList }
        },
        totalCost() {
            return this.store.cartList.reduce((total, cart) => {
                return total + cart.quantity * this.getProduct(cart.productId).price
            }, 0)
        }
    },
    methods: {
        getProduct(productId) {
            return this.store.productList.filter(product => product.id == productId)[0]
        },
        formatPrice(price) {
            return price.toLocaleString('it-IT', { style: 'currency', currency: 'VND' })
        },
        handleIncrement(productId) {
            const cart = store.cartList.filter(cartItem => cartItem.productId == productId)[0]
            const product = this.getProduct(productId)
            cart.quantity += cart.quantity == product.quantityInStock ? 0 : 1
        },
        handleDecrement(productId) {
            const cart = store.cartList.filter(cartItem => cartItem.productId == productId)[0]
            if (cart.quantity > 1)
                cart.quantity--
        },
        handleRemove(productId) {
            store.cartList = store.cartList.filter(cart => cart.productId != productId)
        }
    }
}
</script>

<style scoped></style>