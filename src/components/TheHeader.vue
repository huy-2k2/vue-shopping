<template>
    <header class="header">
        <a class="header-logo" href="#">TurnCart</a>
        <div class="header-right">
            <div class="header-search">
                <input type="text" placeholder="Search" class="header-search-input">
                <button class="header-search-button">Search</button>
            </div>
            <div class="header-cart" @click="handleOpenModal">
                <span class="header-cart-icon">
                    <svg xmlns="http://www.w3.org/2000/svg" class="ionicon" viewBox="0 0 512 512">
                        <title>Cart</title>
                        <circle cx="176" cy="416" r="16" fill="none" stroke="currentColor" stroke-linecap="round"
                            stroke-linejoin="round" stroke-width="32" />
                        <circle cx="400" cy="416" r="16" fill="none" stroke="currentColor" stroke-linecap="round"
                            stroke-linejoin="round" stroke-width="32" />
                        <path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                            stroke-width="32" d="M48 80h64l48 272h256" />
                        <path d="M160 288h249.44a8 8 0 007.85-6.43l28.8-144a8 8 0 00-7.85-9.57H128" fill="none"
                            stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="32" />
                    </svg>
                </span>
                <span class="header-cart-number">{{ totalCart }}</span>
            </div>
        </div>
        <Teleport v-if="isOpenModal" to="#app">
            <TheModal :handleCloseModal="handleCloseModal">
                <ThePayment></ThePayment>
            </TheModal>
        </Teleport>
    </header>
</template>

<script>
import store from '@/store';
import TheModal from './TheModal.vue';
import ThePayment from '@/ThePayment.vue';
export default {
    components: { TheModal, ThePayment },
    data() {
        return {
            isOpenModal: false
        }
    },
    computed: {
        totalCart() {
            return store.cartList.reduce((total, current) => total + current.quantity, 0)
        }
    },
    methods: {
        handleCloseModal() {
            this.isOpenModal = false
        },
        handleOpenModal() {
            this.isOpenModal = true
        }
    }
}
</script>

<style scoped>
.header {
    padding: 12px 24px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #343a43;
}

.header-logo {
    font-size: x-large;
    font-weight: bold;
    background-image: -webkit-linear-gradient(#f00, #0f0);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}

.header-right {
    display: flex;
    align-items: stretch;
    justify-content: start;
    column-gap: 8px;
}

.header-search {
    display: flex;
    align-items: stretch;
    justify-content: start;
    column-gap: 4px;
}

.header-search-input {
    padding: 8px 12px;
    font-size: medium;
    color: #333;
    border: none;
    outline: none;
    border-radius: 4px;
}

.header-search-button {
    background: none;
    border-radius: 4px;
    color: green;
    border: 2px solid green;
    font-weight: bold;
    padding: 0 8px;
}

.header-cart {
    background-color: red;
    display: flex;
    flex-shrink: 0;
    align-items: center;
    justify-content: start;
    padding: 0 12px;
    border-radius: 4px;
    column-gap: 4px;
    cursor: pointer;
}

.header-cart-icon {
    color: white;
    width: 18px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: large;
}

.header-cart-number {
    background-color: white;
    padding: 0px 6px;
    border-radius: 4px;
    font-weight: bold;
}
</style>