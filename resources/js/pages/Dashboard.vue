<script setup>
import Ppdb from "../components/sections/Ppdb.vue";   

defineProps({
    pesan: String,
});
</script>

<template>
    <Ppdb />
    <div class="p-8">
        <h1 class="text-3xl font-bold text-blue-600">{{ pesan }}</h1>
    </div>
</template>