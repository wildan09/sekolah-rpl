<script setup>
import { ref, computed } from "vue";

const currentPage = ref(1);
const itemsPerPage = 6;

const ekstrakurikulerList = [
    {
        nama: "Prakarsa",
        deskripsi:
            "Prakarsa merupakan ambalan Pramuka SMKN 1 Purwosari, terdiri dari Untung Suropati dan R.A. Kartini.",
        gambar: "/images/ekstrakurikuler/prakarsa.jpg",
        logo: "/images/ekstrakurikuler/logo-prakarsa.png",
        link: "#",
    },
    {
        nama: "Paskanusa",
        deskripsi:
            "PASKANUSA merupakan ekstrakurikuler Paskibra SMKN 1 Purwosari yang berdiri sejak 18 Oktober 2002.",
        gambar: "/images/ekstrakurikuler/paskanusa.jpg",
        logo: "/images/ekstrakurikuler/logo-paskanusa.png",
        link: "#",
    },
    {
        nama: "PMR",
        deskripsi:
            "PMR merupakan ekstrakurikuler yang berfokus pada pertolongan pertama, kesehatan, donor darah, dan kemanusiaan.",
        gambar: "/images/ekstrakurikuler/pmr.jpg",
        logo: "/images/ekstrakurikuler/logo-pmr.png",
        link: "#",
    },
    {
        nama: "Broadcasting",
        deskripsi:
            "X-Gen Broadcasting (BC) adalah ekstrakurikuler videografi, presenter, karya visual di SMKN 1 Purwosari.",
        gambar: "/images/ekstrakurikuler/broadcasting.jpg",
        logo: "/images/ekstrakurikuler/logo-broadcasting.png",
        link: "#",
    },
    {
        nama: "MCC",
        deskripsi:
            "Metamorph Creative Crew (MCC) merupakan ekstrakurikuler jurnalistik di bidang fotografi, desain, dan dokumentasi.",
        gambar: "/images/ekstrakurikuler/mcc.jpg",
        logo: "/images/ekstrakurikuler/logo-mcc.png",
        link: "#",
    },
    {
        nama: "Pecinta Alam",
        deskripsi:
            "Yang biasa dikenal dengan Degdayapala, berfokus pada kegiatan alam bebas, wall climbing, dan kepedulian lingkungan, dls.",
        gambar: "/images/ekstrakurikuler/pecinta-alam.jpg",
        logo: "/images/ekstrakurikuler/logo-pecinta-alam.png",
        link: "#",
    },
    // Tambahkan data ekstrakurikuler lain di bawah ini
];

const totalPages = computed(() =>
    Math.ceil(ekstrakurikulerList.length / itemsPerPage),
);

const paginatedEkstrakurikuler = computed(() => {
    const start = (currentPage.value - 1) * itemsPerPage;
    return ekstrakurikulerList.slice(start, start + itemsPerPage);
});

const paginationPages = computed(() => {
    const total = totalPages.value;
    const current = currentPage.value;

    if (total <= 5) {
        return Array.from({ length: total }, (_, i) => i + 1);
    }
    if (current <= 3) {
        return [1, 2, "...", total - 1, total];
    }
    if (current >= total - 2) {
        return [1, 2, "...", total - 1, total];
    }
    return [1, "...", current, "...", total];
});

const goToPage = (page) => {
    currentPage.value = page;
};

const previousPage = () => {
    if (currentPage.value > 1) currentPage.value--;
};

const nextPage = () => {
    if (currentPage.value < totalPages.value) currentPage.value++;
};
</script>

<template>
    <section class="w-full px-6 py-10 lg:px-27.5">
        <!-- Header -->
        <div class="flex flex-col items-center text-center">
            <div class="mb-2 flex items-center gap-2">
                <span class="text-[#FFC107]">
                    <!-- Ganti dengan SVG icon asli dari Figma jika ada -->
                    <svg
                        width="28"
                        height="28"
                        viewBox="0 0 24 24"
                        fill="none"
                        stroke="currentColor"
                        stroke-width="2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        xmlns="http://www.w3.org/2000/svg"
                    >
                        <path d="m11 17 2 2a1 1 0 1 0 3-3" />
                        <path
                            d="m14 14 2.5 2.5a1 1 0 1 0 3-3l-3.88-3.88a3 3 0 0 0-4.24 0l-.88.88a1 1 0 1 1-3-3l2.81-2.81a5.79 5.79 0 0 1 7.06-.87l.47.28a2 2 0 0 0 1.42.25L21 4"
                        />
                        <path d="m21 3 1 11h-2" />
                        <path d="M3 3 2 14l6.5 6.5a1 1 0 1 0 3-3" />
                        <path d="M3 4h8" />
                    </svg>
                </span>

                <span class="text-[18px] font-bold uppercase text-[#1F2937]">
                    Ekstrakurikuler
                </span>
            </div>

            <h2
                class="max-w-158.25 text-[40px] font-bold leading-[1.2] tracking-[-0.02em] text-[#1F2937]"
            >
                Kembangkan Bakat, Raih Prestasi Bersama Ekstrakurikuler
            </h2>
        </div>

        <!-- Grid kartu -->
        <div
            class="mx-auto mt-10 grid max-w-200 grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3"
        >
            <a
                v-for="item in paginatedEkstrakurikuler"
                :key="item.nama"
                :href="item.link"
                class="group block overflow-hidden rounded-[10px] bg-white shadow-[0_2px_12px_rgba(0,0,0,0.06)] transition duration-300 hover:-translate-y-1 hover:shadow-[0_6px_20px_rgba(0,0,0,0.1)]"
            >
                <!-- Foto -->
                <div class="h-33 w-full overflow-hidden">
                    <img
                        :src="item.gambar"
                        :alt="item.nama"
                        class="h-full w-full object-cover transition duration-500 group-hover:scale-105"
                    />
                </div>

                <!-- Konten -->
                <div class="px-4 pb-4 pt-3">
                    <div class="flex items-center justify-between gap-3">
                        <div class="flex min-w-0 items-center gap-3">
                            <img
                                :src="item.logo"
                                :alt="'Logo ' + item.nama"
                                class="h-9 w-9 shrink-0 rounded-full bg-white object-contain"
                            />
                            <h3
                                class="truncate text-[15px] font-semibold text-[#1F2937]"
                            >
                                {{ item.nama }}
                            </h3>
                        </div>

                        <svg
                            width="18"
                            height="18"
                            viewBox="0 0 24 24"
                            fill="none"
                            stroke="#FFC107"
                            stroke-width="2"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            class="shrink-0 transition duration-300 group-hover:translate-x-1"
                            xmlns="http://www.w3.org/2000/svg"
                        >
                            <path d="M5 12h14" />
                            <path d="m13 6 6 6-6 6" />
                        </svg>
                    </div>

                    <p
                        class="mt-3 line-clamp-3 text-[11px] leading-relaxed text-[#A3A3A3]"
                    >
                        {{ item.deskripsi }}
                    </p>
                </div>
            </a>
        </div>

        <!-- Pagination -->
        <div v-if="totalPages > 1" class="mt-8 flex justify-center">
            <div class="flex items-center gap-2">
                <!-- Previous -->
                <button
                    type="button"
                    @click="previousPage"
                    :disabled="currentPage === 1"
                    class="flex h-6 w-6 shrink-0 items-center justify-center rounded-[4px] border border-[#D1D5DB] bg-white text-[#9CA3AF] transition-all duration-200 hover:border-[#FFD000] hover:bg-[#FFFBEA] disabled:cursor-not-allowed disabled:border-[#B8B8B8] disabled:bg-[#B8B8B8] disabled:text-white disabled:hover:bg-[#B8B8B8]"
                    aria-label="Halaman sebelumnya"
                >
                    <svg
                        width="5"
                        height="8"
                        viewBox="0 0 10 16"
                        fill="none"
                        xmlns="http://www.w3.org/2000/svg"
                    >
                        <path
                            d="M9 1L2 8L9 15"
                            stroke="currentColor"
                            stroke-width="2.5"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                        />
                    </svg>
                </button>

                <!-- Nomor halaman -->
                <template v-for="(page, index) in paginationPages" :key="index">
                    <span
                        v-if="page === '...'"
                        class="flex h-6 w-6 shrink-0 items-center justify-center rounded-[4px] border border-[#D1D5DB] bg-white text-[10px] font-medium text-[#1F2937]"
                    >
                        ...
                    </span>

                    <button
                        v-else
                        type="button"
                        @click="goToPage(page)"
                        :class="[
                            'flex h-6 w-6 shrink-0 items-center justify-center rounded-[4px] border text-[10px] font-medium transition-all duration-200',
                            currentPage === page
                                ? 'border-[#FFD000] bg-white text-[#FFD000]'
                                : 'border-[#D1D5DB] bg-white text-[#1F2937] hover:border-[#FFD000] hover:bg-[#FFFBEA] hover:text-[#FFD000]',
                        ]"
                    >
                        {{ page }}
                    </button>
                </template>

                <!-- Next -->
                <button
                    type="button"
                    @click="nextPage"
                    :disabled="currentPage === totalPages"
                    class="flex h-6 w-6 shrink-0 items-center justify-center rounded-[4px] border border-[#D1D5DB] bg-white text-[#9CA3AF] transition-all duration-200 hover:border-[#FFD000] hover:bg-[#FFFBEA] disabled:cursor-not-allowed disabled:border-[#B8B8B8] disabled:bg-[#B8B8B8] disabled:text-white disabled:hover:bg-[#B8B8B8]"
                    aria-label="Halaman berikutnya"
                >
                    <svg
                        width="5"
                        height="8"
                        viewBox="0 0 10 16"
                        fill="none"
                        xmlns="http://www.w3.org/2000/svg"
                    >
                        <path
                            d="M1 1L8 8L1 15"
                            stroke="currentColor"
                            stroke-width="2.5"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                        />
                    </svg>
                </button>
            </div>
        </div>
    </section>
</template>
