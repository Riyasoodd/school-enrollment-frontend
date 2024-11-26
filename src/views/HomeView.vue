<template>
  <div class="home">
    <h1>School Enrollment App</h1>

    <!-- Lesson List Component with Sorting/Filtering -->
    <LessonList :lessons="lessons" @addToCart="addToCart" />

    <!-- Cart Component -->
    <Cart :cart="cartItems" @removeFromCart="removeFromCart" @checkout="checkout" />
  </div>
</template>

<script>
import LessonList from '@/components/LessonList.vue';
import Cart from '@/components/Cart.vue';

export default {
  name: 'HomeView',
  components: {
    LessonList,
    Cart
  },
  data() {
  return {
    lessons: [
      { id: 1, subject: "Math", location: "London", price: 10, spaces: 5 },
      { id: 2, subject: "Science", location: "New York", price: 15, spaces: 2 },
      { id: 3, subject: "English", location: "Bristol", price: 8, spaces: 10 },
      { id: 4, subject: "Music", location: "Oxford", price: 7, spaces: 8 },
      { id: 5, subject: "Art", location: "London", price: 9, spaces: 6 }
      // Add more items as needed
    ],
    cartItems: []
  };
},
  methods: {
    addToCart(lesson) {
      const index = this.cartItems.findIndex((item) => item.id === lesson.id);
      if (index === -1 && lesson.spaces > 0) {
        this.cartItems.push(lesson);
      } else {
        alert('Lesson is either already in the cart or has no available spaces.');
      }
    },
    removeFromCart(lesson) {
      this.cartItems = this.cartItems.filter((item) => item.id !== lesson.id);
    },
    checkout(name, phone) {
      if (name && phone) {
        alert(`Checkout complete for ${name} with phone: ${phone}.`);
        this.cartItems = [];
      } else {
        alert('Please provide a name and phone number for checkout.');
      }
    }
  }
};
</script>

<style scoped>
.home {
  padding: 20px;
}
</style>
