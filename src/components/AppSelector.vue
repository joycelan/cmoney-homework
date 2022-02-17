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
    <div class="title-panel" @click="toggle">
      <div class="title">
        {{ value || title }}
      </div>
      <div class="arrow" :class="{opened: show}"></div>
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
  display: block;
  position: relative;
  background: var(--normal-panel-bg);
  cursor: pointer;
}
.title-panel {
  display: flex;
  width: 200px;
  height: 50px;
  margin-left: 20px;

  .title {
    flex: 1;
    height: 100%;
    width: 100%;
    line-height: 100%;
    display: flex;
    align-items: center;
  }
  .arrow {
    width: 0;
    height: 0;
    margin: 10px;
    margin-top: 20px;
    border-style: solid;
    border-width: 8px 5px 0 5px;
    border-color: #000000 transparent transparent transparent;
    &.opened {
      border-width: 0 5px 8px 5px;
      border-color: transparent transparent #000000 transparent;
    }
  }
}
.dropdown {
  display: block;
  background: white;
  position: absolute;
  width: 100%;
  span {
    display: block;
    width: 100%;
    line-height: 50px;
    margin-left: 20px;
  }
}
</style>
