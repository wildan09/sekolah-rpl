<script setup>
import Navbar from "../layouts/Navbar.vue";

defineProps({
    pesan: String,
});
</script>

<template>
    <Navbar />
    <div class="p-8">
        <h1 class="text-3xl font-bold text-blue-600">{{ pesan }}</h1>
    </div>
</template>