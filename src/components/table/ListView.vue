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
      <tr class="header">
        <td>編號</td>
        <td>行政區域</td>
        <td>鄉鎮區</td>
        <td>商家</td>
        <td class="address">地址</td>
      </tr>
    </thead>

    <tbody>
      <tr v-for="(item, key) in info" :key="key" class="content">
        <td>{{ item.ID }}</td>
        <td>{{ item.City }}</td>
        <td>{{ item.Town }}</td>
        <td>{{ item.Name }}</td>
        <td :title="item.Address" class="ellipsis">
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
  td {
    border: 1px solid;
    border-color: var(--normal-line);
    padding: 0 10px;
    text-align: center;
  }
  .header td {
    background: var(--light-panel-bg);
    &.address {
      width: 50%;
    }
  }
  td {
    max-width: 100px;
  }
}
</style>
