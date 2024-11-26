<template>
  <div class="lesson-card">
    <div class="icon">
      <i :class="getIconClass(lesson.subject)"></i>
    </div>
    <div>
      <h4>Subject: {{ lesson.subject }}</h4>
      <p>Location: {{ lesson.location }}</p>
      <p>Price: £{{ lesson.price }}</p>
      <p>Spaces: {{ lesson.spaces }}</p>
    </div>
    <button @click="handleClick">{{ buttonLabel }}</button>
  </div>
</template>

<script>
export default {
  props: {
    lesson: Object,
    buttonLabel: String,
    onClick: Function,
  },
  methods: {
    handleClick() {
      this.onClick(this.lesson);
    },
    getIconClass(subject) {
      switch (subject) {
        case 'Math':
          return 'fas fa-calculator';
        case 'English':
          return 'fas fa-pen';
        case 'Music':
          return 'fas fa-music';
        default:
          return 'fas fa-book';
      }
    },
  },
};
</script>

<style>
.lesson-card {
  border: 2px solid #ccccff;
  border-radius: 12px;
  padding: 16px;
  margin: 8px;
  width: 200px;
  text-align: center;
  font-family: Arial, sans-serif;
}

.icon {
  font-size: 2rem;
  margin-bottom: 8px;
}

button {
  background-color: #4a90e2;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  margin-top: 12px;
}

button:hover {
  background-color: #357abd;
}
</style>
