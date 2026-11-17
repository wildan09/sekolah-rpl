<script setup>
import Navbar from "../layouts/Navbar.vue";
import Footer from "../layouts/Footer.vue";
import Hero from "../components/sections/Hero.vue";   

defineProps({
    pesan: String,
});
</script>

<template>
    <Navbar />
    <Hero />
    <Footer />
    <div class="p-8">
        <h1 class="text-3xl font-bold text-blue-600">{{ pesan }}</h1>
    </div>
</template>