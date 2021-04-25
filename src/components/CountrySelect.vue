<template>
  <select
    @change="selectCountry()"
    v-model="selected"
    class="mt-10 block w-full border p-3 rounded"
  >
    <option value="0">Select Country</option>
    <option v-for="country in countries" :key="country.ID" :value="country.ID">
      {{ country.Country }}
    </option>
  </select>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "CountrySelect",
  props: {
    countries: {
      type: Array,
    },
  },
  data() {
    return {
      selected: 0,
    };
  },
  methods: {
    selectCountry() {
      const country = this.$props.countries?.find(
        (item: any) => item.ID === this.selected
      );
      this.$emit("get-country", country);
    },
  },
});
</script>
