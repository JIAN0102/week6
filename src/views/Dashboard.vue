<template>
  <div>
    <div id="nav">
      <router-link to="/admin/">後台首頁</router-link> |
      <router-link to="/admin/products">產品列表</router-link> |
      <router-link to="/admin/orders">購物車列表</router-link> |
      <router-link to="/">回到前台</router-link>
    </div>
    <router-view :token="token" v-if="checkSuccess" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      token: '',
      checkSuccess: false,
    };
  },
  created() {
    this.checkAuth();
  },
  methods: {
    checkAuth() {
      this.token = document.cookie.replace(/(?:(?:^|.*;\s*)token\s*=\s*([^;]*).*$)|^.*$/, '$1');
      this.$http.defaults.headers.common.Authorization = `Bearer ${this.token}`;

      const api = `${process.env.VUE_APP_APIPATH}/auth/check`;
      this.$http.post(api, {
        api_token: this.token,
      }).then(() => {
        this.checkSuccess = true;
      }).catch(() => {
        this.$router.push('/login');
      });
    },
  },
};
</script>
