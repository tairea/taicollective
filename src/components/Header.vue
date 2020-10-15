<template>
  <header class="header">
    <g-link to="/" exact class="tohu"> 
   <img src="/uploads/tohu-white-nobg.png" width="150"/>
   </g-link>
  </header>
</template>

<script>
import data from "@/data/theme.json";

export default {
  name: "Header",
  data() {
    return {
      data
    };
  },
  computed: {
    siteName() {
      return data.header_title.split(" ");
    },
    multiLine() {
      return this.siteName.length >= 1;
    }
  }
};
</script>

<style lang="scss" scoped>
.header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 4rem 2rem 2rem 2rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  z-index: 100;
  opacity: 1;
  mix-blend-mode: difference;
  transition: opacity 0.5s ease;
  &.hidden {
    opacity: 0;
  }
}
.tohu {
  font-size: 1rem;
  font-weight: 500;
  user-select: none;
  margin: 0;
  cursor: pointer;
}

a:hover {
  border:none
}

a {
  border: none;
  transition: none;
}
</style>