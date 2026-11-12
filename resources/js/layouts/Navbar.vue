<script setup>
import { ref } from "vue";
import { Link } from "@inertiajs/vue3";

const isMobileOpen = ref(false);
const activeDropdown = ref(null); 

const menuItems = [
    { key: "beranda", label: "Beranda", href: "/" },
    {
        key: "profil",
        label: "Profil",
        children: [
            { label: "Tentang", href: "/profil/tentang" },
            { label: "Struktur", href: "/profil/struktur" },
            { label: "Jurusan", href: "/profil/jurusan" },
        ],
    },
    {
        key: "layanan",
        label: "Layanan",
        children: [
            { label: "PKL", href: "/layanan/pkl" },
            { label: "BKK", href: "/layanan/bkk" },
        ],
    },
   {
        key: "informasi",
        label: "Informasi",
        children: [
            { label: "Berita", href: "/berita" },
            { label: "Artikel", href: "/artikel" },
        ],
    },
    { key: "ppdb", label: "PPDB", href: "/ppdb" },
    {
        key: "blud",
        label: "BLUD",
        children: [
            { label: "SPM BLUD", href: "/blud/spm" },
            { label: "E-Commerce", href: "/blud/ecommerce" },
        ],
    },
];

function toggleDropdown(key) {
    activeDropdown.value = activeDropdown.value === key ? null : key;
}

function closeAll() {
    activeDropdown.value = null;
    isMobileOpen.value = false;
}
</script>

<template>
    <header class="bg-[#132133] text-white sticky top-0 z-50">
        <div class="max-w-[1440px] mx-auto px-[110px] py-6 flex items-center justify-between">
            <!-- Logo -->
            <Link href="/" class="flex items-center gap-3" @click="closeAll">
                <img src="/images/logo-sekolah.webp" alt="Logo Sekolah" class="h-[69px] w-[71px] object-contain" />
                <span class="font-poppins font-bold text-xl leading-tight">
                    SMK NEGERI 1<br />PURWOSARI
                </span>
            </Link>

            <nav class="hidden lg:flex items-center gap-8">
                <template v-for="item in menuItems" :key="item.key">
                    <Link
                        v-if="!item.children"
                        :href="item.href"
                        class="text-lg font-normal hover:text-primary-50 hover:underline hover:font-bold transition-colors"
                    >
                        {{ item.label }}
                    </Link>

                    <!-- Item dengan dropdown -->
                    <div v-else class="relative">
                        <button
                            @click="toggleDropdown(item.key)"
                            class="flex items-center gap-1 text-lg font-normal hover:text-primary-50 hover:font-bold hover:underline transition-colors cursor-pointer"
                        >
                            {{ item.label }}
                            <svg class="h-4 w-4 transition-transform" :class="{ 'rotate-180': activeDropdown === item.key }" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                            </svg>
                        </button>

                        <div
                            v-if="activeDropdown === item.key"
                            class="absolute top-full mt-2 left-0 bg-[#132133] rounded-md shadow-lg min-w-[235px]"
                        >
                            <Link
                                v-for="child in item.children"
                                :key="child.href"
                                :href="child.href"
                                class="block px-[10px] py-[10px] text-lg hover:text-primary-50 hover:font-bold"
                                @click="closeAll"
                            >
                                {{ child.label }}
                            </Link>
                        </div>
                    </div>
                </template>
            </nav>

            <!-- Search + Hamburger -->
            <div class="flex items-center gap-3">
                <button aria-label="Cari" class="p-2 hover:text-amber-400">
                    <svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-4.35-4.35m0 0A7.5 7.5 0 104.35 4.35a7.5 7.5 0 0012.3 12.3z" />
                    </svg>
                </button>
                <button @click="isMobileOpen = !isMobileOpen" class="lg:hidden p-2" aria-label="Toggle menu">
                    <svg v-if="!isMobileOpen" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
                    </svg>
                    <svg v-else class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>
        </div>

        <!-- Menu Mobile -->
        <nav v-if="isMobileOpen" class="lg:hidden bg-[#0f1729] border-t border-white/10 px-4 py-3 flex flex-col gap-1">
            <template v-for="item in menuItems" :key="item.key">
                <Link v-if="!item.children" :href="item.href" class="py-2 text-sm font-medium hover:text-amber-400" @click="closeAll">
                    {{ item.label }}
                </Link>
                <div v-else>
                    <button @click="toggleDropdown(item.key)" class="w-full flex justify-between items-center py-2 text-sm font-medium">
                        {{ item.label }}
                        <svg class="h-3 w-3" :class="{ 'rotate-180': activeDropdown === item.key }" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                        </svg>
                    </button>
                    <div v-if="activeDropdown === item.key" class="pl-4 flex flex-col gap-1 pb-2">
                        <Link v-for="child in item.children" :key="child.href" :href="child.href" class="py-1 text-sm text-gray-300 hover:text-amber-400" @click="closeAll">
                            {{ child.label }}
                        </Link>
                    </div>
                </div>
            </template>
        </nav>
    </header>
</template>