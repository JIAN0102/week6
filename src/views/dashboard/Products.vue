<template>
  <div>
    <loading :active.sync="isLoading"></loading>
    <ul>
      <li v-for="product in products" :key="product.id">
        <h2>{{ product.title }}</h2>
        <p>{{ product.content }}</p>
      </li>
    </ul>
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
  props: {
    token: {
      type: String,
      default: '',
    },
  },
  created() {
    this.isLoading = true;
    const api = `${process.env.VUE_APP_APIPATH}/${process.env.VUE_APP_UUID}/admin/ec/products`;
    this.$http.get(api).then((res) => {
      this.products = res.data.data;
      this.isLoading = false;
    }).catch(() => {
    });
  },
};
</script>
