<script>
import ModeSwitch from "./table/ModeSwitch.vue";
import ListSnapView from "./table/ListSnapView.vue";
import ListView from "./table/ListView.vue";

export default {
  components: {
    ModeSwitch,
    ListSnapView,
    ListView,
  },
  props: {
    info: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      countPerPage: 10,
      pageIndex: 1,
      mode: "snap",
      modeList: ["snap", "list", "card"],
    };
  },
  watch: {
    info() {
      this.pageIndex = 1;
    },
  },
  computed: {
    pageInfo() {
      const pad = (this.pageIndex - 1) * this.countPerPage;
      return this.info.slice(pad, pad + this.countPerPage);
    },
    pageCount() {
      return Math.ceil(this.info.length / this.countPerPage);
    },
  },
  methods: {
    setMode(mode) {
      this.mode = mode;
    },
    setPage(index) {
      this.pageIndex = index;
    },
  },
};
</script>

<template>
  <ModeSwitch :options="modeList" :value="mode" @change="setMode" />
  <ListView v-if="mode === 'list'" :info="pageInfo" />
  <ListSnapView v-if="mode === 'snap'" :info="pageInfo" />
  <div class="footer">
    <div>
      {{ `美食頁次 ${pageIndex}/${pageCount}` }}
    </div>
    <div
      class="page"
      :class="{ active: pageIndex === index }"
      v-for="index in pageCount"
      :key="index"
      @click="setPage(index)"
    >
      {{ index }}
    </div>
  </div>
</template>

<style scoped lang="less">
@import "@/assets/base.css";

.footer {
  display: flex;
  div {
    margin: 5px;
    line-height: 30px;
    &.page {
      display: inline-block;
      width: 30px;
      background: var(--light-panel-bg);
      text-align: center;
      cursor: pointer;
      &.active {
        background: var(--active-panel-bg);
      }
    }
  }
}
</style>
