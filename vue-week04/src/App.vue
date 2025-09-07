<template>
  <div id="app" class="container py-4">
    <div class="row">
      <!-- 商品列表區 -->
      <ProductList></ProductList>

      <!-- 購物車區 -->
      <Cart></Cart>
    </div>

    <!-- 通知元件 -->
    <NotificationVue></NotificationVue>
  </div>
</template>

<script setup>
import ProductList from "./components/ProductList.vue";
import Cart from "./components/Cart.vue";
import Notification from "./components/Notification.vue";
</script>
