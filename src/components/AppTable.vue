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
      pageIndex: 1,
    };
  },
  watch: {
    info() {
      this.pageIndex = 1;
    }
  },
  computed: {
    pageInfo() {
      const pad = (this.pageIndex -1) * this.countPerPage;
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
      <tr>
        <th>編號</th>
        <th>行政區域</th>
        <th>鄉鎮區</th>
        <th>商家</th>
        <th>地址</th>
      </tr>
      <tr v-for="(item, key) in pageInfo" :key="key" class="content">
        <td>{{ item.ID }}</td>
        <td>{{ item.City }}</td>
        <td>{{ item.Town }}</td>
        <td>{{ item.Name }}</td>
        <td :title="item.Address" class="address ellipsis">
          {{ item.Address }}
        </td>
      </tr>
    </tbody>
  </table>
  <div class="footer">
    <div>
      {{ `美食頁次 ${pageIndex}/${pageCount}` }}
    </div>
    <div
      class="page"
      :class="{active: pageIndex === index}"
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

.table {
  border-collapse: collapse;
  tr {
    line-height: 40px;
    border: 1px solid;
    &.content:nth-child(odd) {
      background: var(--pale-panel-bg);
    }
    &.content:hover {
      background: var(--hover-panel-bg);
    }
  }
  td,
  th {
    border: 1px solid;
    border-color: var(--normal-line);
    padding: 0 20px;
    text-align: center;
  }
  th {
    background: var(--light-panel-bg);
  }
  td {
    max-width: 100px;
  }
}
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
