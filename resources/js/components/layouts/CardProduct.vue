<script setup>
import { ref, computed } from "vue";

const currentPage = ref(1);
const itemsPerPage = 12;

const produkList = [
    {
        id: 1,
        nama: "Bibit Tanaman Cabai",
        harga: 25000,
        deskripsi: "Bibit berkualitas untuk kebutuhan budidaya.",
        gambar: "/images/produk/bibit-cabai.jpg",
        link: "#",
    },
    {
        id: 2,
        nama: "Bibit Tanaman Tomat",
        harga: 25000,
        deskripsi: "Bibit berkualitas untuk kebutuhan budidaya.",
        gambar: "/images/produk/bibit-tomat.jpg",
        link: "#",
    },
    {
        id: 3,
        nama: "Bibit Tanaman Terong",
        harga: 25000,
        deskripsi: "Bibit berkualitas untuk kebutuhan budidaya.",
        gambar: "/images/produk/bibit-terong.jpg",
        link: "#",
    },
    {
        id: 4,
        nama: "Bibit Tanaman Selada",
        harga: 25000,
        deskripsi: "Bibit berkualitas untuk kebutuhan budidaya.",
        gambar: "/images/produk/bibit-selada.jpg",
        link: "#",
    },
    {
        id: 5,
        nama: "Bibit Tanaman Kangkung",
        harga: 25000,
        deskripsi: "Bibit berkualitas untuk kebutuhan budidaya.",
        gambar: "/images/produk/bibit-kangkung.jpg",
        link: "#",
    },
    {
        id: 6,
        nama: "Bibit Tanaman Bayam",
        harga: 25000,
        deskripsi: "Bibit berkualitas untuk kebutuhan budidaya.",
        gambar: "/images/produk/bibit-bayam.jpg",
        link: "#",
    },
    {
        id: 7,
        nama: "Bibit Tanaman Sawi",
        harga: 25000,
        deskripsi: "Bibit berkualitas untuk kebutuhan budidaya.",
        gambar: "/images/produk/bibit-sawi.jpg",
        link: "#",
    },
    {
        id: 8,
        nama: "Bibit Tanaman Timun",
        harga: 25000,
        deskripsi: "Bibit berkualitas untuk kebutuhan budidaya.",
        gambar: "/images/produk/bibit-timun.jpg",
        link: "#",
    },
    {
        id: 9,
        nama: "Pupuk Organik Cair",
        harga: 35000,
        deskripsi: "Pupuk organik untuk menyuburkan tanaman.",
        gambar: "/images/produk/pupuk-cair.jpg",
        link: "#",
    },
    {
        id: 10,
        nama: "Pot Tanaman",
        harga: 15000,
        deskripsi: "Pot berkualitas untuk berbagai jenis tanaman.",
        gambar: "/images/produk/pot.jpg",
        link: "#",
    },
    {
        id: 11,
        nama: "Media Tanam",
        harga: 20000,
        deskripsi: "Campuran tanah dan kompos siap pakai.",
        gambar: "/images/produk/media-tanam.jpg",
        link: "#",
    },
    {
        id: 12,
        nama: "Paket Hidroponik",
        harga: 120000,
        deskripsi: "Paket lengkap hidroponik untuk pemula.",
        gambar: "/images/produk/hidroponik.jpg",
        link: "#",
    },
    {
        id: 13,
        nama: "Bibit Tanaman Melon",
        harga: 30000,
        deskripsi: "Bibit berkualitas untuk kebutuhan budidaya.",
        gambar: "/images/produk/bibit-melon.jpg",
        link: "#",
    },
    {
        id: 14,
        nama: "Bibit Tanaman Semangka",
        harga: 30000,
        deskripsi: "Bibit berkualitas untuk kebutuhan budidaya.",
        gambar: "/images/produk/bibit-semangka.jpg",
        link: "#",
    },
];

const formatRupiah = (angka) => "Rp" + Number(angka).toLocaleString("id-ID");
const totalPages = computed(() => Math.ceil(produkList.length / itemsPerPage));

const paginatedProduk = computed(() => {
    const start = (currentPage.value - 1) * itemsPerPage;
    return produkList.slice(start, start + itemsPerPage);
});

const paginationPages = computed(() => {
    const total = totalPages.value;
    const current = currentPage.value;

    if (total <= 5) {
        return Array.from({ length: total }, (_, i) => i + 1);
    }
    if (current <= 3 || current >= total - 2) {
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
    <section class="w-full px-4 py-10 sm:px-8 sm:py-14 lg:px-27.5">
        <div class="mx-auto max-w-[1160px]">
            <div>
                <h2
                    class="text-[28px] font-bold leading-[1.2] tracking-[-0.02em] text-[#1F2937] sm:text-[34px] lg:text-[40px]"
                >
                    Produk Terbaru
                </h2>
                <p class="mt-1 text-[16px] text-[#A3A3A3] sm:text-[20px]">
                    Produk terbaru dari berbagai jurusan
                </p>
            </div>
            <div
                class="mt-6 grid grid-cols-1 gap-4 sm:grid-cols-2 sm:gap-5 lg:grid-cols-3 xl:grid-cols-4"
            >
                <article
                    v-for="produk in paginatedProduk"
                    :key="produk.id"
                    class="group flex flex-col overflow-hidden rounded-[10px] bg-white shadow-[0_2px_12px_rgba(0,0,0,0.06)] transition duration-300 hover:-translate-y-1 hover:shadow-[0_8px_24px_rgba(0,0,0,0.10)]"
                >
                    <div
                        class="aspect-[1.87/1] w-full overflow-hidden bg-gray-100"
                    >
                        <img
                            :src="produk.gambar"
                            :alt="produk.nama"
                            loading="lazy"
                            class="h-full w-full object-cover transition duration-500 group-hover:scale-105"
                        />
                    </div>
                    <div class="flex flex-1 flex-col px-4 pb-4 pt-3">
                        <h3
                            class="truncate text-[15px] font-semibold text-[#1F2937]"
                        >
                            {{ produk.nama }}
                        </h3>

                        <p class="mt-1 text-[12px] font-medium text-[#FFC107]">
                            {{ formatRupiah(produk.harga) }}
                        </p>

                        <p
                            class="mt-2 line-clamp-2 min-h-[2.8em] text-[11px] leading-[1.4] text-[#A3A3A3]"
                        >
                            {{ produk.deskripsi }}
                        </p>

                        <a
                            :href="produk.link"
                            class="mt-auto inline-flex w-fit items-center gap-2 pt-3 text-[10px] font-medium text-[#FFC107] transition hover:text-[#e0a800]"
                        >
                            Lihat Detail
                            <svg
                                width="14"
                                height="14"
                                viewBox="0 0 24 24"
                                fill="none"
                                stroke="currentColor"
                                stroke-width="2"
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                class="transition duration-300 group-hover:translate-x-1"
                                xmlns="http://www.w3.org/2000/svg"
                            >
                                <path d="M5 12h14" />
                                <path d="m13 6 6 6-6 6" />
                            </svg>
                        </a>
                    </div>
                </article>
            </div>
            <div v-if="totalPages > 1" class="mt-8 flex justify-center">
                <div class="flex items-center gap-1.5 sm:gap-2">
                    <button
                        type="button"
                        @click="previousPage"
                        :disabled="currentPage === 1"
                        class="flex h-7 w-7 shrink-0 items-center justify-center rounded-[4px] border border-[#D1D5DB] bg-white text-[#9CA3AF] transition-all duration-200 hover:border-[#FFD000] hover:bg-[#FFFBEA] disabled:cursor-not-allowed disabled:border-[#B8B8B8] disabled:bg-[#B8B8B8] disabled:text-white disabled:hover:bg-[#B8B8B8] sm:h-6 sm:w-6"
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

                    <template
                        v-for="(page, index) in paginationPages"
                        :key="index"
                    >
                        <span
                            v-if="page === '...'"
                            class="flex h-7 w-7 shrink-0 items-center justify-center rounded-[4px] border border-[#D1D5DB] bg-white text-[10px] font-medium text-[#1F2937] sm:h-6 sm:w-6"
                        >
                            ...
                        </span>
                        <button
                            v-else
                            type="button"
                            @click="goToPage(page)"
                            :class="[
                                'flex h-7 w-7 shrink-0 items-center justify-center rounded-[4px] border text-[10px] font-medium transition-all duration-200 sm:h-6 sm:w-6',
                                currentPage === page
                                    ? 'border-[#FFD000] bg-white text-[#FFD000]'
                                    : 'border-[#D1D5DB] bg-white text-[#1F2937] hover:border-[#FFD000] hover:bg-[#FFFBEA] hover:text-[#FFD000]',
                            ]"
                        >
                            {{ page }}
                        </button>
                    </template>

                    <button
                        type="button"
                        @click="nextPage"
                        :disabled="currentPage === totalPages"
                        class="flex h-7 w-7 shrink-0 items-center justify-center rounded-[4px] border border-[#D1D5DB] bg-white text-[#9CA3AF] transition-all duration-200 hover:border-[#FFD000] hover:bg-[#FFFBEA] disabled:cursor-not-allowed disabled:border-[#B8B8B8] disabled:bg-[#B8B8B8] disabled:text-white disabled:hover:bg-[#B8B8B8] sm:h-6 sm:w-6"
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
        </div>
    </section>
</template>
