<script setup>
import VisiMisiCard from '../components/ui/VisiMisiCard.vue'
import SearchBar from '../components/ui/SearchBar.vue'

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
    </main>
</template>