<script>
export default {
  props: {
    info: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<template>
  <table class="table">
    <thead>
      <tr>
        <th>編號</th>
        <th>行政區域</th>
        <th>鄉鎮區</th>
        <th>商家</th>
        <th>地址</th>
      </tr>
    </thead>

    <tbody>
      <tr v-for="(item, key) in info" :key="key" class="content">
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
  thead th {
    border: 1px solid;
    border-color: var(--normal-line);
    padding: 0 20px;
    text-align: center;
  }
  thead th {
    background: var(--light-panel-bg);
  }
  td {
    max-width: 100px;
  }
}
</style>
