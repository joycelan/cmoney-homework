<script>
import axios from "axios";
import Table from "@/components/AppTable.vue";
import Select from "@/components/AppSelector.vue";
import AdPanel from "@/components/AppAdPanel.vue";

export default {
  props: {},
  components: {
    Table,
    Select,
    AdPanel,
  },
  data() {
    return {
      rawData: [],
      info: [],
      isLoading: true,
      map: {},
      city: "",
      town: "",
    };
  },
  computed: {
    townList() {
      if (!this.city) {
        return [];
      }
      return this.map[this.city];
    },
    cityList() {
      return Object.keys(this.map);
    },
  },
  watch: {
    city() {
      console.log(this.city);
      this.setInfo();
    },
    town() {
      console.log(this.town);
      this.setInfo();
    },
  },
  mounted() {
    this.getInfo();
  },
  methods: {
    setCity(city) {
      this.city = city;
      this.town = "";
    },
    setTown(town) {
      this.town = town;
    },
    setInfo() {
      this.info = this.rawData.filter((e) => {
        if (!this.city) return true;
        return this.town
          ? e.City === this.city && e.Town === this.town
          : e.City === this.city;
      });
      console.log(this.info, this.city, this.town);
    },
    setMap() {
      this.info.forEach((e) => {
        if (!this.map[e.City]) {
          this.map[e.City] = [];
        }
        if (this.map[e.City].indexOf(e.Town) === -1) {
          this.map[e.City].push(e.Town);
        }
      });
    },
    render(info) {
      this.rawData = info;
      this.setInfo();
      this.setMap();
    },
    getInfo() {
      axios
        .get(
          "https://data.coa.gov.tw/Service/OpenData/ODwsv/ODwsvTravelFood.aspx"
        )
        .then((response) => {
          // handle success
          this.render(response.data);
          this.isLoading = false;
        })
        .catch(function (error) {
          // handle error
          console.log(error);
        })
        .then(function () {
          // always executed
        });
    },
  },
};
</script>

<template>
  <div v-if="isLoading" class="load">{{ "Loading..." }}</div>
  <div v-else class="app">
    <div class="main">
      <div class="nav">
        <Select
          title="請選擇行政區域"
          :options="cityList"
          @change="setCity"
          :value="city"
        />
        <Select
          title="請選擇鄉鎮區"
          :options="townList"
          @change="setTown"
          :value="town"
        />
      </div>

      <Table :info="info" />
    </div>
    <AdPanel class="ad" />
  </div>
</template>

<style lang="less">
@import "@/assets/base.css";

#app {
  width: 100%;
  height: 100%;
  .app {
    display: flex;
  }
  .main {
    flex: 1;
    .nav {
      display: flex;
    }
  }
  .ad {
    width: 300px;
  }
}
.selector {
  width: 240px;
  margin: 10px;
}
</style>
