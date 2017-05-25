<template>
  <div id="app">
    <div class="header">
      <v-header :seller="seller"></v-header>
    </div>
    <div class="tabs">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import header from './components/header/Header.vue'

const ERR_OK = 0;

export default {
  name: 'app',
  data() {
    return {
        seller: {}
    }
  },
  created() {
    this.$http.get('/api/seller').then((response) => {
      response = response.body;
      if (response.errno === ERR_OK) {
        this.seller = response.data;
        console.log(this.seller);
      }
    });
  },
  components: {
    'v-header': header
  }
}
</script>

<style>
#app .tabs {
  display: flex;
  width: 100%;
  height: 40px;
  line-height: 40px;
  border-bottom: 1px solid rgba(7, 17, 27, 0.1);
}

.tab-item {
  flex: 1;
  text-align: center;
}

.tab-item > a {
  display: block;
  font-size: 14px;
  color: rgb(77, 85, 93);
}

.tab-item .active {
  color: rgb(240, 20, 20);
}
</style>
