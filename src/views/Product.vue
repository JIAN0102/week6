<template>
  <div>
    <loading :active.sync="isLoading"></loading>
    <h1>{{ product.title }}</h1>
    <p>{{ product.content }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isLoading: false,
      product: {},
    };
  },
  created() {
    this.isLoading = true;
    const { id } = this.$route.params;
    const api = `${process.env.VUE_APP_APIPATH}/${process.env.VUE_APP_UUID}/ec/product/${id}`;
    this.$http.get(api).then((res) => {
      this.isLoading = false;
      this.product = res.data.data;
    });
  },
};
</script>
