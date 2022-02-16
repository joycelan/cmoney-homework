<script>
import axios from "axios";
import Table from "@/components/AppTable.vue";
import Select from "@/components/AppSelector.vue";

export default {
  props: {},
  components: {
    Table,
    Select,
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
  methods: {
    setCity(city) {
      this.city = city;
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
  <div>
    <button @click="getInfo">
      {{ "Get info" }}
    </button>
    <div class="nav">
      <Select title="請選擇市" :options="cityList" @change="setCity" />
      <Select title="請選擇鄉鎮區" :options="townList" @change="setTown" />
    </div>

    <Table :info="info" />
  </div>
</template>

<style>
@import "@/assets/base.css";

.nav {
  display: flex;
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }
}
</style>
