<script>
export default {
  props: {
    info: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    openUrl(url) {
      if (!url) return;
      window.open(url, "_blank");
    },
  },
};
</script>

<template>
  <div class="table">
    <div
      v-for="(item, key) in info"
      :key="key"
      @click="openUrl(item.Url)"
      class="item"
    >
      <div class="head">
        <div class="city">
          {{ item.City }}
        </div>
        <div class="town">
          {{ item.Town }}
        </div>
      </div>
      <div class="content">
        <img :src="item.PicURL" />
        <div>
          <div class="title">
            {{ item.Name }}
          </div>
          <div class="detail" :title="item.FoodFeature">
            {{ item.FoodFeature }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="less">
@import "@/assets/base.css";

.table {
  display: flex;
  flex-direction: column;
  background-color: var(--light-panel-bg);
  .item {
    display: flex;
    flex-direction: row;
    margin: 10px;
  }
  .head {
    margin: 0 10px 0 10px;
    flex: 1;
    display: flex;
    flex-direction: column;
    .city {
      width: 40px;
      color: white;
      padding: 5px;
      background-color: var(--active-panel-bg);
      font-size: 12px;
      margin-bottom: 10px;
    }
    .town {
      width: 20px;
      align-self: end;
      color: var(--normal-text-color);
    }
  }
  .content {
    display: flex;
    background-color: white;
    padding: 10px;
    &:hover {
      .title {
        color: var(--hover-text-color);
      }
    }
    img {
      height: auto;
      max-width: 100px;
    }
    .title {
      text-align: left;
      margin: 15px;
      font-size: 20px;
    }
    .detail {
      margin: 10px;
      color: var(--normal-text-color);
      -webkit-line-clamp: 3;
      display: -webkit-box;
      -webkit-box-orient: vertical;
      overflow: hidden;
    }
  }
}
</style>
