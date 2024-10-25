<template>
    <ul class="grid gap-y-4 p-3">
        <span v-for="message in messages" :key="message?.id" :class="message?.author === 'me' ? 'max-w-[70%] p-2 border rounded-md bg-gradient-to-r from-fuchsia-600 to-purple-600 text-white justify-self-end' : 'max-w-[70%] p-2 border border-gray-300 rounded-md justify-self-start'">
            {{ message?.message }}
        </span>
    </ul>
</template>

<script setup>
import { storeToRefs } from "pinia";
import { useStore } from "../store";
const store = useStore();

const { messages } = storeToRefs(store);
</script>

<style>

</style>