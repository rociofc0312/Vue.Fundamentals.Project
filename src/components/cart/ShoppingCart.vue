<template src='./ShoppingCart.html'></template>
<style lang='scss' scoped src='./ShoppingCart.scss'></style>

<script>
export default {
  name: 'Cart',
  computed: {
    cart() {
      return this.$store.state.cart;
    },
  },
};
</script>
