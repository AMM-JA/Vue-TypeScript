<script lang="ts">
import type Entry from "@/types/Entry";
import formatRelative from "date-fns/formatRelative";
import { defineComponent, type PropType } from "vue";
export default defineComponent({
  props: {
    // date: { type: Object as PropType<Entry>, required: true },
    date: { type: Date, required: true },
  },
  // emits:{
  //   doSomething(payload :Entry){
  //     return true;
  //   }
  // },
  computed: {
    formatted(): string {
      return formatRelative(this.date, Date.now());
    },
  },
  mounted() {
    this.$http("https://myendpoint.com");
    // ! https://vuejs.org/guide/typescript/options-api.html#augmenting-custom-options
    // this.formatted;
  },
});
</script>
<template>
  <div>{{ formatted }}</div>
</template>
