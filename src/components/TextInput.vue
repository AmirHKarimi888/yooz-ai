<template>

    <form @submit.prevent="sendMessage" class="flex items-center max-w-lg mx-auto w-[80%]">
        <label for="text-input" class="sr-only">Search</label>
        <div class="relative w-full">
            <input type="text" id="text-input" v-model="message"
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full ps-10 p-2.5"
                placeholder="Write a message..." required />
            <button @click="sendMessage" type="button" class="absolute inset-y-0 end-0 flex items-center pe-3">
                <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24">
                    <path fill="currentColor" d="M3 20v-6l8-2l-8-2V4l19 8z" />
                </svg>
            </button>
        </div>
    </form>

</template>

<script setup>
import { ref } from "vue";
import youz from "../youz";
import { storeToRefs } from "pinia";
import { useStore } from "../store";

const store = useStore();

const { messages } = storeToRefs(store);

const message = ref("");

let youzParser = new youz();
const inputCode = `
#Iraq : A country in Western Asia.
verbs {is, was, became, went, came}
pronouns {I, you, he, she, we, they}
(
    + Hi*1
    - Hello*1
)
(
    + Hello*1
    - Hi*1
)
(
    + What is your name?
    - My name is yooz.
)
(
    + How are you?
    - I'm good, thanks for asking.
)
(
    + How's it going?
    - Thank you _ I appreciate it _ How about you?
)
(
    + Where is Iraq?
    - #Iraq
)
- {from, to, with, in}
(
    + suitcase
    - Understood
)
(
    + My name is *1.
    - Nice to meet you, *1.
)
(
    + I travel to city *2 *1 times a year.
    - Do you enjoy traveling to city *2 *1 times a year?
)
(
    + {Iraq, country}
    - #Iraq
)
(
    + Tell me about yourself.
    - I'm good !>
)
(
    + &pronoun &verb.
    - You used a pronoun and a verb.
)
`;
youzParser.parse(inputCode);


const sendMessage = () => {
    const newMessage = {
        id: Math.round(Math.random() * 10000000000),
        message: message.value,
        author: "me"
    }

    if (message.value) {
        messages.value.push(newMessage);

        const response = youzParser.getResponse(message.value);
        const newResponse = {
            id: Math.round(Math.random() * 10000000000),
            message: response,
            author: "him"
        }
        messages.value.push(newResponse);

        message.value = "";
    }
}
</script>

<style></style>