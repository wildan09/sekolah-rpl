<script setup lang="ts">
import LulusanTerbaik, { type Graduate } from "../components/sections/LulusanTerbaik.vue";

defineProps<{ pesan?: string }>();

const graduates: Graduate[] = [
    { id: 1, label: "RPL", name: "Muhammad Sumbul Jetian", major: "Rekayasa Perangkat Lunak", graduationYear: 2025, job: "Programmer", motivation: "Terus belajar dan berkembang." },
    { id: 2, label: "DKV", name: "Nama DKV", major: "Desain Komunikasi Visual", graduationYear: 2025, job: "Desainer", motivation: "Contoh motivasi." },
    { id: 3, label: "TKJ", name: "Nama TKJ", major: "Teknik Komputer dan Jaringan", graduationYear: 2024, job: "Network Engineer", motivation: "Contoh motivasi." },
    { id: 4, label: "TKR", name: "Nama TKR", major: "Teknik Kendaraan Ringan", graduationYear: 2024, job: "Mekanik", motivation: "Contoh motivasi." },
];

</script>

<template>
    <LulusanTerbaik :items="graduates" />
</template>