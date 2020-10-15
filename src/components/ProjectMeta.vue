<template>
  <section class="project-meta">
    <h2 class="project-title">{{ title }}</h2>
    <ul class="project-categories">
      <li
        class="project-category"
        v-for="(category, index) in categories"
        :key="index"
      >
        {{ category }}
      </li>
    </ul>
    <time class="project-year" :datetime="year">{{ year }}</time>
  </section>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: false
    },
    categories: {
      type: Array,
      required: false
    },
    year: {
      type: String,
      required: false
    }
  }
};
</script>

<style lang="scss" scoped>
.project-meta {
  padding: 2rem 0;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  line-height: 1.5;
  flex-direction: column;
  display: flex;
  height: 100%;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  @media (max-width: 599px) {
    padding: 0;
    align-items: center;
  }
  
}
.project-title {
  font-size: 1rem;
  font-weight: 500;
  margin: 0;
}
.project-categories {
  padding: 0;
  margin: 0;
  list-style: none;
}
.project-category {
  padding: 0;
  margin: 0;
}
.project-year {
  text-align: right;
}
</style>