<script setup lang="ts">
import TheHeader from "@/components/TheHeader.vue";
import EntryEditor from "./components/EntryEditor.vue";
import EntryCard from "@/components/EntryCard.vue";
import { reactive, provide, inject } from "vue";
import type User from "./types/User";
import type Emoji from "./types/Emoji";
import type Entry from "./types/Entry";

const entries: Entry[] = reactive([]);

const user: User = reactive({
  id: 1,
  username: "Aung Myat Moe",
  settings: [],
});
console.log(user.id);

// ? Injection !
import type { InjectionKey } from "vue";
import { userInjectionKey } from "./injectionKeys";
// const userInjectionKey = Symbol() as InjectionKey<User>;
provide(userInjectionKey,user)

// *** in child component
// const injectedUser = inject (userInjectionKey) ;

const handleCreateEntry = (entry: Entry) => {
  // console.log("entry", entry);
  entries.unshift(entry);
};
</script>

<template>
  <main class="container m-auto p-10">
    <TheHeader />
    <EntryEditor @@create="handleCreateEntry" />
    <ul>
      <li v-for="entry in entries" :key="entry.id">
        <EntryCard :entry="entry" />
      </li>
    </ul>
  </main>
</template>
