<template>
  <div>
    <loading :active.sync="isLoading"></loading>
    <table>
      <tr v-for="product in products" :key="product.id">
        <td>{{ product.title }}</td>
        <td>{{ product.content }}</td>
        <td>
          <router-link :to="`/product/${product.id}`">看產品細節</router-link>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isLoading: false,
      products: [],
    };
  },
  created() {
    this.isLoading = true;
    const api = `${process.env.VUE_APP_APIPATH}/${process.env.VUE_APP_UUID}/ec/products`;
    this.$http.get(api).then((res) => {
      this.isLoading = false;
      this.products = res.data.data;
    });
  },
};
</script>
