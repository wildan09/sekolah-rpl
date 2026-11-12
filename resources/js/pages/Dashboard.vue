<script setup>
import VisiMisiCard from '../components/ui/VisiMisiCard.vue'
import SearchBar from '../components/ui/SearchBar.vue'
import CardDaftarGuru from '../components/ui/CardDaftarGuru.vue'
import CardStruktur from '../components/ui/CardStruktur.vue'
import FasilitasSection from '../components/section/FasilitasSection.vue'
import SpmbSection from '../components/sections/SpmbSection.vue'
import Ppdb from '../components/sections/Ppdb.vue'
import Navbar from '../layouts/Navbar.vue'
import Footer from '../layouts/Footer.vue'

defineProps({
    pesan: String,
})
</script>

<template>
    <main class="p-8">
        <VisiMisiCard />

        <div class="mt-8 max-w-xl">
            <SearchBar />
        </div>

        <CardDaftarGuru />
        <CardStruktur />
        <FasilitasSection />
        <SpmbSection />
        <Ppdb />
        <Navbar />
         <Footer />
        <div class="p-8">
            <h1 class="text-3xl font-bold text-blue-600">{{ pesan }}</h1>
        </div>
    </main>
    <Footer />
</template>