<script setup>
import { Link } from "@inertiajs/vue3";
import ArtikelCard from "@/Components/layouts/ArtikelCard.vue";

defineProps({
    articles: {
        type: Array,
        default: () => [
            {
                id: 1,
                title: "Mengenal Metaverse: Arti, Cara Kerja, dan Opsi Kegiatan di Dalamnya",
                date: "4 Maret 2023",
                datetime: "2023-03-04",
                href: "#",
                thumbnail: null,
            },
            {
                id: 2,
                title: "Daihatsu Skill Contest Regional Jatim Bali",
                date: "4 Maret 2023",
                datetime: "2023-03-04",
                href: "#",
                thumbnail: null,
            },
            {
                id: 3,
                title: "Mengenal Metaverse: Arti, Cara Kerja, dan Opsi Kegiatan di Dalamnya",
                date: "4 Maret 2023",
                datetime: "2023-03-04",
                href: "#",
                thumbnail: null,
            },
            {
                id: 4,
                title: "Daihatsu Skill Contest Regional Jatim Bali",
                date: "4 Maret 2023",
                datetime: "2023-03-04",
                href: "#",
                thumbnail: null,
            },
        ],
    },
    allHref: { type: String, default: "#" },
});
</script>

<template>
    <section
        id="artikel"
        aria-labelledby="artikel-heading"
        class="bg-white py-16 sm:py-20 lg:py-24"
    >
        <div class="mx-auto max-w-[1200px] px-4 sm:px-6 lg:px-8">
            <header class="mx-auto max-w-3xl text-center">
                <p
                    class="text-[24px] font-bold uppercase text-primary-60 sm:text-[24px] lg:text-[24px]"
                >
                    Artikel
                </p>
                <h2
                    id="artikel-heading"
                    class="text-[48px] font-bold mt-1.5 text-secondary-60"
                >
                    Segala Informasi Terbaru
                </h2>
                <p
                    class="mt-1.5 text-2xl leading-snug text-neutral-40 sm:text-lg lg:text-2xl"
                >
                    Dapatkan berbagai informasi terbaru seputar kegiatan,
                    prestasi, pengumuman, dan kabar lainnya dari SMK Negeri 1
                    Purwosari.
                </p>
            </header>

            <div
                class="mt-[42px] grid grid-cols-1 gap-6.5 sm:mt-10 sm:gap-6 lg:grid-cols-2"
            >
                <ArtikelCard
                    v-for="article in articles"
                    :key="article.id"
                    :article="article"
                />
            </div>

            <div class="mt-15 flex justify-center sm:mt-12">
                <Link
                    :href="allHref"
                    class="inline-flex items-center justify-center gap-4 whitespace-nowrap rounded-xl bg-primary-60 px-5 py-3 text-sm font-semibold text-secondary-60 transition-colors duration-300 hover:bg-primary-50 sm:gap-5 sm:px-6 sm:py-3.5 sm:text-base"
                >
                    Lihat Selengkapnya

                    <svg
                        class="shrink-0 transition-transform duration-300 ease-out group-hover:translate-x-1.5 group-focus-visible:translate-x-1.5 motion-reduce:transition-none motion-reduce:transform-none"
                        width="18"
                        height="15"
                        viewBox="0 0 18 15"
                        fill="none"
                        xmlns="http://www.w3.org/2000/svg"
                        aria-hidden="true"
                    >
                        <path d="M5 12h14" />
                        <path d="m13 6 6 6-6 6" />
                    </svg>
                </Link>
            </div>
        </div>
    </section>
</template>
