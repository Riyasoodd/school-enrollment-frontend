<template>
  <div>
    <h2>Shopping Cart</h2>
    <div class="cart-container">
      <LessonCard
        v-for="lesson in cart"
        :key="lesson.id"
        :lesson="lesson"
        buttonLabel="Remove"
        :onClick="removeFromCart"
      />
    </div>
    <h3>Checkout</h3>
    <form @submit.prevent="checkout">
      <label for="name">Name:</label>
      <input v-model="name" type="text" id="name" />
      <label for="phone">Phone:</label>
      <input v-model="phone" type="text" id="phone" />
      <button type="submit">Checkout</button>
    </form>
  </div>
</template>

<script>
import LessonCard from "./LessonCard.vue";

export default {
  components: { LessonCard },
  props: {
    cart: Array,
  },
  data() {
    return {
      name: "",
      phone: "",
    };
  },
  methods: {
    removeFromCart(lesson) {
      this.$emit("removeFromCart", lesson);
    },
    checkout() {
      // Implement checkout logic here
      this.$emit("checkout", this.name, this.phone);
    },
  },
};
</script>

<style>
.cart-container {
  display: flex;
  gap: 16px;
}
form {
  display: flex;
  gap: 8px;
  align-items: center;
}
</style>
