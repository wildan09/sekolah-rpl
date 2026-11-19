<script setup>
import { computed } from "vue";
import CardProgramKeahlian from "../ui/CardProgramKeahlianJs.vue";

const props = defineProps({
    // TODO: hapus dummy ini saat integrasi data asli
    programs: {
        type: Array,
        default: () => [
            {
                id: 1,
                title: "Rekayasa Perangkat Lunak",
                description:
                    "Rekayasa Perangkat Lunak mempelajari pembuatan aplikasi, website, dan sistem informasi dengan bekal pemrograman serta pengembangan perangkat lunak modern.",
                category: "Teknologi Informatika",
                tone: "primary",
                image: null,
                href: "#",
            },
            {
                id: 2,
                title: "Teknik Komputer dan Jaringan",
                description:
                    "Teknik Komputer dan Jaringan mempelajari perakitan komputer, instalasi sistem operasi, konfigurasi jaringan LAN/WAN, server, hingga keamanan jaringan.",
                category: "Teknologi Informatika",
                tone: "primary",
                image: null,
                href: "#",
            },
            {
                id: 3,
                title: "Desain Komunikasi Visual",
                description:
                    "Desain Komunikasi Visual mempelajari seni desain grafis, teknik ilustrasi, fotografi, videografi, serta media cetak dan digital untuk menyampaikan pesan secara kreatif.",
                category: "Teknologi Informatika",
                tone: "primary",
                image: null,
                href: "#",
            },
            {
                id: 4,
                title: "Teknik Kendaraan Ringan",
                description:
                    "Teknik Kendaraan Ringan mempelajari perawatan, perbaikan, serta sistem kelistrikan dan mesin pada kendaraan roda empat atau mobil secara mendalam.",
                category: "Teknologi dan Rekayasa",
                tone: "blue",
                image: null,
                href: "#",
            },
            {
                id: 5,
                title: "Teknik Bodi Kendaraan Ringan",
                description:
                    "Teknik Bodi Kendaraan Ringan mempelajari teknik perbaikan, pengecatan, serta restorasi rangka dan bodi kendaraan akibat benturan atau kerusakan bodi mobil.",
                category: "Teknologi dan Rekayasa",
                tone: "blue",
                image: null,
                href: "#",
            },
            {
                id: 6,
                title: "Teknik Pemesinan",
                description:
                    "Teknik Pemesinan mempelajari proses pengoperasian mesin produksi seperti mesin bubut, frais, CNC, serta teknik perancangan komponen logam industri.",
                category: "Teknologi dan Rekayasa",
                tone: "blue",
                image: null,
                href: "#",
            },
        ],
    },
    lastPage: { type: Number, default: 2 },
});

// v-model:page dari parent, atau state lokal bila tidak diikat.
const currentPage = defineModel("page", { type: Number, default: 1 });

function goTo(page) {
    currentPage.value = Math.min(Math.max(page, 1), props.lastPage);
}

const pageItems = computed(() => {
    const last = props.lastPage;
    const current = currentPage.value;

    const pages = [
        ...new Set([1, 2, last - 1, last, current - 1, current, current + 1]),
    ]
        .filter((p) => p >= 1 && p <= last)
        .sort((a, b) => a - b);

    const items = [];
    pages.forEach((p, i) => {
        if (i > 0 && p - pages[i - 1] > 1) {
            items.push({ type: "gap", key: `gap-${p}` });
        }
        items.push({ type: "page", value: p, key: `page-${p}` });
    });
    return items;
});
</script>

<template>
    <section
        id="program-keahlian"
        aria-labelledby="program-heading"
        class="bg-white py-16 sm:py-20 lg:py-24"
    >
        <div class="mx-auto max-w-[1200px] px-4 sm:px-6 lg:px-8">
            <header class="mx-auto max-w-xl text-center">
                <h2 id="program-heading" class="heading-2 text-secondary-60">
                    Program Keahlian
                </h2>
                <p
                    class="mt-3 text-base leading-snug text-neutral-40 sm:text-lg lg:text-xl"
                >
                    SMK Negeri 1 Purwosari memiliki berbagai program keahlian
                    yang dapat kamu pilih sesuai minat dan bakatmu.
                </p>
            </header>

            <div
                v-if="programs.length"
                class="mt-8 grid grid-cols-1 justify-items-center gap-4 sm:mt-10 sm:grid-cols-2 sm:gap-6 lg:grid-cols-3"
            >
                <CardProgramKeahlian
                    v-for="program in programs"
                    :key="program.id"
                    :program="program"
                />
            </div>
            <p v-else class="mt-10 text-center text-neutral-40">
                Belum ada data.
            </p>

            <nav
                v-if="lastPage > 1"
                aria-label="Navigasi halaman"
                class="mt-8 flex items-center justify-center gap-1.5 sm:mt-10 sm:gap-2"
            >
                <button
                    type="button"
                    aria-label="Halaman sebelumnya"
                    :disabled="currentPage <= 1"
                    class="flex size-8 items-center justify-center rounded border border-neutral-30 bg-white text-neutral-50 transition-colors hover:border-primary-60 hover:text-primary-60 disabled:cursor-not-allowed disabled:border-neutral-30 disabled:bg-neutral-30 disabled:text-white"
                    @click="goTo(currentPage - 1)"
                >
                    <svg
                        class="size-4"
                        viewBox="0 0 24 24"
                        fill="none"
                        stroke="currentColor"
                        stroke-width="2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        aria-hidden="true"
                    >
                        <path d="m15 6-6 6 6 6" />
                    </svg>
                </button>

                <template v-for="item in pageItems" :key="item.key">
                    <span
                        v-if="item.type === 'gap'"
                        class="flex size-8 items-center justify-center rounded border border-neutral-30 text-xs text-neutral-50"
                        aria-hidden="true"
                    >
                        …
                    </span>
                    <button
                        v-else
                        type="button"
                        :aria-current="
                            item.value === currentPage ? 'page' : undefined
                        "
                        :aria-label="`Halaman ${item.value}`"
                        class="flex size-8 items-center justify-center rounded border text-xs transition-colors"
                        :class="
                            item.value === currentPage
                                ? 'border-primary-60 font-semibold text-primary-60'
                                : 'border-neutral-30 text-secondary-60 hover:border-primary-60'
                        "
                        @click="goTo(item.value)"
                    >
                        {{ item.value }}
                    </button>
                </template>

                <button
                    type="button"
                    aria-label="Halaman berikutnya"
                    :disabled="currentPage >= lastPage"
                    class="flex size-8 items-center justify-center rounded border border-neutral-30 bg-white text-neutral-50 transition-colors hover:border-primary-60 hover:text-primary-60 disabled:cursor-not-allowed disabled:border-neutral-30 disabled:bg-neutral-30 disabled:text-white"
                    @click="goTo(currentPage + 1)"
                >
                    <svg
                        class="size-4"
                        viewBox="0 0 24 24"
                        fill="none"
                        stroke="currentColor"
                        stroke-width="2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        aria-hidden="true"
                    >
                        <path d="m9 6 6 6-6 6" />
                    </svg>
                </button>
            </nav>
        </div>
    </section>
</template>