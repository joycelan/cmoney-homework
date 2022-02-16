<script>
export default {
  props: {
    info: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      countPerPage: 10,
      pageIndex: 0,
    };
  },
  computed: {
    pageInfo() {
      const pad = this.pageIndex * this.countPerPage;
      return this.info.slice(pad, pad + this.countPerPage);
    },
    pageCount() {
      return Math.ceil(this.info.length / this.countPerPage);
    },
  },
  methods: {
    setPage(index) {
      this.pageIndex = index;
    },
  },
};
</script>

<template>
  <table class="table">
    <thead></thead>
    <tbody>
      <tr v-for="(item, key) in pageInfo" :key="key">
        <td>{{ item.ID }}</td>
        <td>{{ item.Name }}</td>
        <td>{{ item.Address }}</td>
      </tr>
    </tbody>
  </table>
  <div class="footer">
    <div
      class="page"
      v-for="index in pageCount"
      :key="index"
      @click="setPage(index - 1)"
    >
      {{ index }}
    </div>
  </div>
</template>

<style>
@import "@/assets/base.css";
</style>
