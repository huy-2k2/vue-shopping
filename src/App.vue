<template>
  <TheHeader></TheHeader>
  <ProductList></ProductList>
</template>

<script>
import ProductList from './components/ProductList.vue';
import TheHeader from './components/TheHeader.vue';


export default {
  name: 'App',
  components: {
    TheHeader,
    ProductList
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
