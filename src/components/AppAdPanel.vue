<script>
export default {
  data() {
    return {
      count: 3,
      isFixed: false,
    };
  },
  created() {
    window.addEventListener("scroll", this.handleScroll);
  },
  unmounted() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll() {
      const element = document.getElementsByClassName("lastAd")[0];

      const rect = element.getBoundingClientRect();
      const html = document.documentElement;
      if (
        rect.top >= 0 &&
        rect.left >= 0 &&
        rect.bottom <= (window.innerHeight || html.clientHeight) &&
        rect.right <= (window.innerWidth || html.clientWidth)
      ) {
        this.isFixed = true;
      }
    },
  },
};
</script>

<template>
  <div class="panel">
    <div
      v-for="index in count"
      :key="index"
      class="item"
      v-show="(index == count && isFixed) || !isFixed"
      :class="{ lastAd: index === count, fixed: isFixed && index == count }"
    >
      <img :src="`src/assets/adv${index}.png`" />
    </div>
  </div>
</template>

<style scoped lang="less">
@import "@/assets/base.css";

.panel {
  display: flex;
  flex-direction: column;
}
.item {
  margin: 10px;
  img {
    width: 100%;
  }
  &.lastAd {
    &.fixed {
      position: fixed;
      top: 0;
      height: 80vh;
      width: 280px; /* FIX ME */
    }
  }
}
</style>
