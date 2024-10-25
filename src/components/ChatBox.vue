<template>
  <div class="border h-[90%] box-border overflow-auto bg-slate-50">
    <Messages v-if="messages.length !== 0" />
    <div v-else class="text-center mt-40">No messages yet...</div>
  </div>
</template>

<script setup>
import Messages from "./Messages.vue";
import { storeToRefs } from "pinia";
import { useStore } from "../store";
const store = useStore();

const { messages } = storeToRefs(store);
</script>

<style>

</style>