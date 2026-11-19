<script setup>
import ArtikelSection from "@/Components/sections/ArtikelSection.vue";
defineProps({
    pesan: String,
    articles: Array,
});
</script>

<template>
    <ArtikelSection />
</template>
