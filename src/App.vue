<script setup>
import {ref, onMounted} from 'vue';
import PocketBase from 'pocketbase';

const db = new PocketBase('http://127.0.0.1:8090');

const titleVal = ref("");
const descVal = ref("");
const data = ref([]);

async function submit() {
    // example create data
    const record = {
        Title: titleVal.value,
        Description: descVal.value,
    };
    await db.collection('posts').create(record);
    data.value.push(record);
};

onMounted(async() =>{
    const result = await db.collection("posts").getFullList();
    data.value = result;
})

</script>

<template>
    <input class="bg-green-400 px-5 py-1 rounded-lg mx-10 my-2 outline outline-2" v-model="titleVal">
    <input class="bg-yellow-400 px-5 py-1 rounded-lg my-2 outline outline-2" v-model="descVal">
    <br>
    <button class="bg-red-600 text-white px-5 py-2 rounded-lg mx-60 my-2 transition duration-200 hover:bg-red-300" @click ="submit">Submit</button>
    <ul>
        <li v-for="item in data">{{ item.Title }}</li>
    </ul>
    <table>
        <td>
            <tr v-for="item in data">{{ item.Title }}</tr>
        </td>
        <td>
            <tr v-for="item in data">{{ item.Description }}</tr>
        </td>
        
    </table>
</template>