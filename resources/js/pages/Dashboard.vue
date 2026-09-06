<script setup>
defineProps({
    pesan: String,
});
</script>

<template>
    <div class="p-8">
        <h1 class="text-3xl font-bold text-blue-600">{{ pesan }}</h1>
    </div>
</template>
