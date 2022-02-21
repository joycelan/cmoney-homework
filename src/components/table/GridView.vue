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
  <div class="table">
    <div
      v-for="(item, key) in info"
      :key="key"
      class="item"
      :style="{ backgroundImage: 'url(' + item.PicURL + ')' }"
    >
      <div class="cover" />
      <div class="info">
        <div class="content">
          <div class="title">
            {{ item.Name }}
          </div>
          <div class="detail" :title="item.FoodFeature">
            ----------------
            <br />
            {{ item.FoodFeature }}
          </div>
        </div>
        <div class="head">
          <div class="city">
            {{ item.City }}
          </div>
          <div class="town">
            {{ item.Town }}
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
  flex-direction: row;
  flex-wrap: wrap;
  background-color: var(--light-panel-bg);
  .item {
    width: 300px;
    height: 150px;
    background-size: cover;
    background-repeat: no-repeat;
    margin: 20px;
    font-size: 12px;
    color: white;
    position: relative;
    .cover {
      background-color: black;
      opacity: 30%;
      position: relative;
      width: 100%;
      height: 100%;
    }
    .info {
      display: flex;
      flex-direction: column-reverse;
      width: 100%;
      height: 100%;
      position: absolute;
      top: 0;
      left: 0;
    }
    &:hover {
      .cover {
        display: none;
      }
      .info .detail {
        display: -webkit-box;
      }
      background-size: 130%;
    }
  }

  @media (max-width: 768px) {
    .item {
      width: 100%;
    }
  }
  .info {
    .head {
      margin: 0 10px 0 10px;
      display: flex;
      flex-direction: row;
      .city {
        width: 40px;
        padding: 5px;
        background-color: var(--active-panel-bg);
      }
      .town {
        padding: 5px;
      }
    }
    .content {
      margin: 5px 10px;
      .detail {
        display: none;
        -webkit-line-clamp: 3;
        -webkit-box-orient: vertical;
        overflow: hidden;
      }
    }
  }
}
</style>
