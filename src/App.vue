<script setup lang="ts">
import TheHeader from "@/components/TheHeader.vue";
import EntryEditor from "./components/EntryEditor.vue";
import EntryCard from "@/components/EntryCard.vue";
import type Entry from "@/types/Entry";
import {reactive, provide} from "vue";
import type User from "@/types/User";
import { userInjectionKey } from "@/types/injectionKeys"
// data
const entries: Entry[] = reactive([]);
const user = reactive<User>(
    {
      userName: 'Pau',
      id: 1,
      settings: []
    }
)
provide(userInjectionKey, user)
// methods
const handleCreateEntry = (entry: Entry) => {
  entries.unshift(entry);
}
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
