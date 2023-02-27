<script lang="ts" setup>
import EmojiField from "@/components/EmojiField.vue";
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg";
import { ref, computed, onMounted, inject } from "vue";
import type Emoji from "@/types/Emoji";

//? data
const body = ref("");
const emoji = ref<Emoji | null>(null);
const charCount = computed<number>(() => body.value.length);
const maxChars = 280;
const handleTextInput = (e:Event)=>{
  const textarea = e.target as HTMLTextAreaElement;
  if (textarea.value.length <= maxChars) {
    body.value = textarea.value;
  } else {
    body.value = textarea.value = textarea.value.substring(0, maxChars);
  }
}

//? template refs
const textarea = ref<HTMLTextAreaElement | null>(null);
onMounted(() => textarea.value?.focus());
</script>
<template>
  <form class="entry-form" @submit.prevent>
    <textarea
      :value="body"
      ref="textarea"
      @keyup="handleTextInput"
      placeholder="New Journal Entry for danielkelly_io"
    ></textarea>
    <EmojiField v-model="emoji" />
    <div class="entry-form-footer">
      <span>{{ charCount }} / 280</span>
      <button>Remember <ArrowCircleRight width="20" /></button>
    </div>
  </form>
</template>
