<script>
export default {
  props: {
    options: {
      type: Array,
      default: () => [],
    },
    value: {
      type: String,
      default: "",
    },
  },
  data() {
    return {};
  },
  watch: {
    value() {
      console.log(this.value);
    },
  },
  methods: {
    selectItem(option) {
      this.$emit("change", option);
    },
  },
};
</script>

<template>
  <div class="mode-switch">
    <div>
      {{ `檢視模式:` }}
    </div>
    <div
      class="mode"
      v-for="option in options"
      @click="selectItem(option)"
      :key="option"
      :class="{ active: option === value }"
    >
      {{ option }}
    </div>
  </div>
</template>

<style scoped lang="less">
@import "@/assets/base.css";

.mode-switch {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  margin-bottom: 10px;
  div {
    margin: 5px;
    line-height: 30px;
    &.mode {
      display: inline-block;
      width: 30px;
      background: var(--light-panel-bg);
      text-align: center;
      cursor: pointer;
      padding: 0 10px;
      &.active {
        background: var(--active-panel-bg);
      }
    }
  }
}
</style>
