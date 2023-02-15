<script setup>
import { ref } from "vue";
import { invoke } from "@tauri-apps/api/tauri";
import { isTauri } from "../utils/shared";

const greetMsg = ref("");
const name = ref("");

async function greet() {
  // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
  if (isTauri) {
    greetMsg.value = await invoke("greet", { name: name.value });
  } else {
    greetMsg.value = name;
  }
}
</script>

<template>
  <div class="card">
    <input id="greet-input" v-model="name" placeholder="Enter a name..." />
    <button type="button" @click="greet()">Greet</button>
  </div>

  <p>{{ greetMsg }}</p>
</template>
