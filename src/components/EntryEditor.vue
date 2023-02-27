<script lang="ts" setup>
import EmojiField from "@/components/EmojiField.vue";
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg";
import { ref, computed, onMounted, inject } from "vue";
import type Emoji from "@/types/Emoji";

// ? data
const body = ref("");
const emoji = ref<Emoji | null>(null);
const charCount = computed<number>(() => body.value.length);
const maxChars = 280;

// ? emit event
// defineEmits(["@create"]);
const emit = defineEmits<{
  // (e: "@create", entry: Entry): void;
  (
    e: "@create",
    entry: {
      text: string;
      emoji: Emoji | null;
    }
  ): void;
}>();
// https://vuejs.org/guide/typescript/composition-api.htm/#typing-component-emits
const handleSubmit = () => {
  // emit("@create", {
  //   body: body.value,
  //   emoji: emoji.value,
  //   createdAt: new Date(),
  //   userId: 1,
  //   id: Math.random(),
  // });
  // body.value = "";
  // emoji.value = null;
};

// ? methods
const handleTextInput = (e: Event) => {
  const textarea = e.target as HTMLTextAreaElement;
  if (textarea.value.length <= maxChars) {
    body.value = textarea.value;
  } else {
    body.value = textarea.value = textarea.value.substring(0, maxChars);
  }
};

// ? template refs
const textarea = ref<HTMLTextAreaElement | null>(null);
onMounted(() => textarea.value?.focus());
</script>
<template>
  <form class="entry-form" @submit.prevent="handleSubmit">
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
