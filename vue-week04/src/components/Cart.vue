<template>
  <div class="col-md-4">
    <h2 class="mb-3">購物車</h2>
    <div v-if="carts.length === 0" class="text-center text-muted">
      <p>購物車是空的</p>
    </div>
    <ul class="list-group mb-3">
      <li
        v-for="item in carts"
        key="item.id"
        class="list-group-item d-flex justify-content-between align-items-center"
      >
        <div>
          <h6 class="my-0">{{ item.name }}</h6>
          <small class="text-muted">數量：{{ item.amount }}</small>
        </div>
        <div>
          <span class="text-muted">${{ item.amount * item.price }}</span>
          <button class="btn btn-sm btn-outline-danger ms-2">移除</button>
        </div>
      </li>
    </ul>
  </div>
  {{ carts }}
</template>

<script setup>
const props = defineProps({
  carts: {
    type: Array,
    required: true,
  },
});
</script>
