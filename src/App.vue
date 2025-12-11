<script setup>
import { ref, computed } from "vue";

// 1. 定义商品列表
const cartList = ref([
  { id: 1, name: "小米 14 Pro", price: 4999, count: 1, image: "📱" },
  { id: 2, name: "Redmi K70", price: 2499, count: 2, image: "🔥" },
  { id: 3, name: "小米 Su7 模型", price: 299, count: 5, image: "🚗" },
]);

// 2. 定义操作方法：增加数量
const add = (item) => {
  item.count++;
};

// 3. 定义操作方法：减少数量 (判断:不能减到负数)
const minus = (item) => {
  if (item.count > 0) {
    item.count--;
  }
};

// 4. 定义计算属性：总价 (核心中的核心！)
const totalPrice = computed(() => {
  return cartList.value.reduce((sum, item) => {
    return sum + item.price * item.count;
  }, 0);
});
</script>

<template>
  <div class="cart-box">
    <div class="header">
      <h3>我的购物车 Demo</h3>
      <span class="badge">共 {{ cartList.length }} 件商品</span>
    </div>

    <div class="item-list">
      <div class="item" v-for="item in cartList" :key="item.id">
        <div class="info">
          <span class="icon">{{ item.image }}</span>
          <div class="details">
            <div class="name">{{ item.name }}</div>
            <div class="price">¥{{ item.price }}</div>
          </div>
        </div>

        <div class="controls">
          <button @click="minus(item)" :disabled="item.count === 0">-</button>
          <span class="count">{{ item.count }}</span>
          <button @click="add(item)">+</button>
        </div>
      </div>
    </div>

    <div class="footer">
      <span>合计：</span>
      <span class="total-price">¥{{ totalPrice }}</span>
      <button class="pay-btn">去结算</button>
    </div>
  </div>
</template>

<style scoped>
/* 整个购物车卡片 */
.cart-box {
  width: 350px;
  margin: 50px auto;
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  font-family: sans-serif;
}

/* 头部 */
.header {
  background: #ff6900; /* 小米橙 */
  color: white;
  padding: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* 列表项 */
.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px;
  border-bottom: 1px solid #eee;
}

.info {
  display: flex;
  align-items: center;
  gap: 10px;
}

.icon {
  font-size: 24px;
}
.name {
  font-weight: bold;
  color: #333;
}
.price {
  color: #999;
  font-size: 14px;
  margin-top: 4px;
}

/* 按钮区域 */
.controls button {
  width: 25px;
  height: 25px;
  border: 1px solid #ddd;
  background: white;
  border-radius: 4px;
  cursor: pointer;
}
.controls button:active {
  background: #eee;
}
.count {
  margin: 0 10px;
  font-weight: bold;
}

/* 底部 */
.footer {
  padding: 15px;
  background: #f9f9f9;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 10px;
}
.total-price {
  color: #ff6900;
  font-size: 20px;
  font-weight: bold;
}
.pay-btn {
  background: #ff6900;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 20px;
  cursor: pointer;
}
</style>
