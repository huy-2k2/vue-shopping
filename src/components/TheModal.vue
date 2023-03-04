<template>
    <div class="container">
        <div class="modal">
            <div class="heading">
                <span class="heading-text">Cart</span>
                <span @click="handleCloseModal" class="heading-icon">
                    <svg xmlns="http://www.w3.org/2000/svg" class="ionicon" viewBox="0 0 512 512">
                        <title>Close</title>
                        <path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                            stroke-width="32" d="M368 368L144 144M368 144L144 368" />
                    </svg>
                </span>
            </div>
            <div class="body">
                <slot></slot>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        handleCloseModal: {
            type: Function,
            required: true
        }
    }
}
</script>

<style scoped>
.container {
    position: fixed;
    inset: 0;
    background-color: #33333362;
}

.modal {
    width: 600px;
    max-width: 100%;
    padding: 20px;
    margin: 0 auto;
    background-color: white;
    margin-top: 100px;
}

.heading {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-bottom: 10px;
    border-bottom: 1px solid #ccc;
}

.heading-text {
    font-size: larger;
    font-weight: bold;
}

.heading-icon {
    width: 30px;
    height: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    cursor: pointer;
}

.heading-icon:hover {
    background-color: #66666671;
}

.body {
    padding: 10px;
}
</style>