<template>
  <div>
    <loading :active.sync="isLoading"></loading>
    <form class="form-signin" @submit.prevent="signin">
      <h1 class="h3 mb-3 font-weight-normal">
        請先登入
      </h1>
      <div class="form-group">
        <label for="inputEmail" class="sr-only">Email address</label>
        <input id="inputEmail" type="email"
          class="form-control" placeholder="Email address" v-model="user.email"
          required autofocus>
      </div>
      <div class="form-group">
        <label for="inputPassword" class="sr-only">Password</label>
        <input id="inputPassword" type="password" class="form-control"
          placeholder="Password" v-model="user.password" required>
      </div>
      <button class="btn btn-lg btn-primary btn-block" type="submit">
        登入
      </button>
      <br>
      <button class="btn btn-outline-primary btn-block" type="button">
        登出
      </button>
      <br>
      <button class="btn btn-outline-primary btn-block" type="button">
        取得資料
      </button>
      <p class="mt-5 mb-3 text-muted">
        &copy; 2020~∞ - 六角學院
      </p>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isLoading: false,
      user: {
        email: '',
        password: '',
      },
    };
  },
  methods: {
    signin() {
      this.isLoading = true;
      const api = `${process.env.VUE_APP_APIPATH}/auth/login`;
      this.$http.post(api, this.user).then((res) => {
        this.isLoading = false;
        const { token } = res.data;
        const { expired } = res.data;
        // 寫入 cookie token
        // expires 設置有效時間
        document.cookie = `token=${token};expires=${new Date(expired * 1000)};`;
        this.$router.push('/admin');
      }).catch(() => {
      });
    },
  },
};
</script>
