<template>
  <!-- Loading Complete -->
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <DataBoxes :stats="stats" />
    <CountrySelect :countries="countries" @get-country="getCountryData" />

    <button
      v-if="stats.Country"
      @click="setGlobal"
      class="bg-green-400 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-700"
    >
      Global
    </button>
  </main>
  <!-- If Loading -->
  <main class="flex flex-col justify-center items-center" v-else>
    <div class="text-gray-600 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="loadingImage" alt="loading.." class="w-24 m-auto" />
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import DataTitle from "@/components/DataTitle.vue";
import DataBoxes from "@/components/DataBoxes.vue";
import CountrySelect from "@/components/CountrySelect.vue";
export default defineComponent({
  name: "Home",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect,
  },
  data() {
    return {
      loading: true,
      title: "Global Data",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImage: require("@/assets/hourglass.gif"),
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },
    getCountryData(country: any) {
      this.stats = country;
      this.title = country.Country;
    },
    async setGlobal() {
      this.loading = true;
      const data = await this.fetchCovidData();
      this.title = "Global Data";
      this.stats = data.Global;
      this.loading = false;
    },
  },
  async created() {
    const data = await this.fetchCovidData();

    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },
});
</script>
