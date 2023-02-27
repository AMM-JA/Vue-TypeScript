<script lang="ts" setup>
import DateDisplay from "./DateDisplay.vue";
import UseEmojis from "@/composables/UseEmojis";
import type Entry from "@/types/Entry";
const { findEmoji } = UseEmojis();

// ? props
// const props = defineProps({
//   entry : { type : Entry},
//   randomProp: { type: String },
// });
//? type-base-props
defineProps<{
  entry?: Entry;
}>();
</script>
<template>
  <div class="entry-card">
    <div class="entry-card-body">
      <component width="75" :is="findEmoji(entry?.emoji)"></component>
      <div class="entry-text">{{entry?.body}}</div>
    </div>
    <div class="entry-footer">
      <DateDisplay :date="entry?.createdAt" class="mr-2" />
      |
      <span class="ml-2">Aung Myat Moe</span>
    </div>
  </div>
</template>
