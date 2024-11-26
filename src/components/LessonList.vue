<template>
  <div>
    <h2>Sort by</h2>
    <div>
      <label><input type="radio" value="subject" v-model="sortBy" /> Subject</label>
      <label><input type="radio" value="location" v-model="sortBy" /> Location</label>
      <label><input type="radio" value="price" v-model="sortBy" /> Price</label>
      <label><input type="radio" value="availability" v-model="sortBy" /> Availability</label>
    </div>
    <div>
      <label><input type="radio" value="ascending" v-model="order" /> Ascending</label>
      <label><input type="radio" value="descending" v-model="order" /> Descending</label>
    </div>

    <div class="lesson-list">
      <LessonCard
        v-for="lesson in sortedLessons"
        :key="lesson.id"
        :lesson="lesson"
        buttonLabel="Add to Cart"
        :onClick="addToCart"
      />
    </div>
  </div>
</template>

<script>
import LessonCard from "./LessonCard.vue";

export default {
  components: { LessonCard },
  props: {
    lessons: Array,
  },
  data() {
    return {
      sortBy: "subject",
      order: "ascending",
    };
  },
  computed: {
    sortedLessons() {
      return [...this.lessons].sort((a, b) => {
        const modifier = this.order === "ascending" ? 1 : -1;
        if (a[this.sortBy] < b[this.sortBy]) return -1 * modifier;
        if (a[this.sortBy] > b[this.sortBy]) return 1 * modifier;
        return 0;
      });
    },
  },
  methods: {
    addToCart(lesson) {
      this.$emit("addToCart", lesson);
    },
  },
};
</script>

<style>
.lesson-list {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}
</style>
