<template>
  <div class="text-center">
    <h2 class="text-3xl font-bold">
      {{ text }}
    </h2>
    <div class="text-2xl mt-4 mb-10">
      <!-- Date -->
      {{ timestamp }}
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import moment from "moment";
export default defineComponent({
  name: "DataTitle",
  props: {
    text: {
      type: String,
    },
    dataDate: {
      type: String,
    },
  },
  computed: {
    timestamp(): String {
      return moment(this.$props.dataDate).format("MMM Do YYYY, h:mm:ss a");
    },
  },
});
</script>
