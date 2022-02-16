<script>
export default {
  props: {
    options: {
      type: Array,
      default: () => [],
    },
    title: {
      type: String,
      default: "",
    },
    value: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      show: false,
    };
  },
  watch: {
  },
  methods: {
    toggle() {
      this.show = !this.show;
    },
    selectItem(option) {
      this.show = false;
      this.$emit("change", option);
    },
  },
};
</script>

<template>
  <div class="selector">
    <div class="title" @click="toggle">
      {{ value || title }}
    </div>
    <div class="dropdown" v-show="show">
      <span v-for="option in options" @click="selectItem(option)" :key="option">
        {{ option }}
      </span>
    </div>
  </div>
</template>

<style scoped lang="less">
@import "@/assets/base.css";

.selector {
  width: 200px;
  display: block;
  position: relative;
}
.title {
  background: var(--normal-panel-bg);
  width: 100%;
}
.dropdown {
  display: block;
  background: white;
  position: absolute;
  width: 100%;
  span {
    display: block;
    width: 100%;
  }
}
</style>
