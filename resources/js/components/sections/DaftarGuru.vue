<script setup>
import { computed } from "vue";
import CardDaftarGuru from "../layouts/CardDaftarGuru.vue";

const props = defineProps({
    tabs: {
        type: Array,
        default: () => [
            { key: "pimpinan", label: "Pimpinan Sekolah" },
            { key: "kompetensi", label: "Kompetensi Keahlian" },
            { key: "guru", label: "Guru Mata Pelajaran" },
        ],
    },
    teachers: {
        type: Array,
        default: () => [
            {
                id: 1,
                name: "Dr. Hj. Nining Faridah, M.Si.",
                subject: "Matematika",
                photo: null,
            },
            {
                id: 2,
                name: "Dr. Hj. Nining Faridah, M.Si.",
                subject: "Matematika",
                photo: null,
            },
            {
                id: 3,
                name: "Dr. Hj. Nining Faridah, M.Si.",
                subject: "Matematika",
                photo: null,
            },
            {
                id: 4,
                name: "Dr. Hj. Nining Faridah, M.Si.",
                subject: "Matematika",
                photo: null,
            },
            {
                id: 5,
                name: "Dr. Hj. Nining Faridah, M.Si.",
                subject: "Pendidikan Agama Islam",
                photo: null,
            },
            {
                id: 6,
                name: "Dr. Hj. Nining Faridah, M.Si.",
                subject: "Pendidikan Agama Islam",
                photo: null,
            },
            {
                id: 7,
                name: "Dr. Hj. Nining Faridah, M.Si.",
                subject: "Pendidikan Agama Islam",
                photo: null,
            },
            {
                id: 8,
                name: "Dr. Hj. Nining Faridah, M.Si.",
                subject: "Bahasa Indonesia",
                photo: null,
            },
            {
                id: 9,
                name: "Dr. Hj. Nining Faridah, M.Si.",
                subject: "Bahasa Indonesia",
                photo: null,
            },
        ],
    },
    lastPage: { type: Number, default: 10 },
});

const activeTab = defineModel("tab", { type: String, default: "guru" });
const currentPage = defineModel("page", { type: Number, default: 1 });

function selectTab(key) {
    activeTab.value = key;
    currentPage.value = 1;
}

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
        id="struktur-organisasi"
        aria-labelledby="struktur-heading"
        class="bg-white py-16 sm:py-20 lg:py-24"
    >
        <div class="mx-auto max-w-[1200px] px-4 sm:px-6 lg:px-8">
            <header class="mx-auto text-center">
                <div class="flex items-center justify-center gap-3">
                    <span
                        class="h-[4px] w-[73px] rounded-2xl bg-primary-60 sm:w-14"
                        aria-hidden="true"
                    />
                    <p
                        class="text-[20px] font-bold uppercase text-black sm:text-sm lg:text-[20px]"
                    >
                        Struktur Organisasi
                    </p>
                    <span
                        class="h-[4px] w-[73px] rounded-2xl bg-primary-60 sm:w-14"
                        aria-hidden="true"
                    />
                </div>

                <h2
                    id="struktur-heading"
                    class="text-[50px] font-bold mt-[12px] text-secondary-60"
                >
                    SMK Negeri 1 Purwosari
                </h2>
                <p
                    class="mt-[12px] text-[24px] leading-snug text-neutral-40 sm:text-[24px]"
                >
                    Bersama membangun pendidikan vokasi yang unggul,
                    berkarakter, dan berdaya saing.
                </p>
            </header>

            <div
                class="mt-[30px] flex flex-wrap justify-center gap-[16px] sm:mt-8 sm:gap-3"
            >
                <button
                    v-for="tab in tabs"
                    :key="tab.key"
                    type="button"
                    :aria-pressed="activeTab === tab.key"
                    class="rounded-[10px] border px-[20px] py-[10px] text-base font-medium transition-colors duration-300 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-primary-60 sm:px-4 sm:py-2 sm:text-sm"
                    :class="
                        activeTab === tab.key
                            ? 'border-primary-60 bg-primary-60 text-secondary-60 shadow-[0_4px_12px_rgba(255,193,7,0.35)]'
                            : 'border-neutral-20 bg-white text-secondary-60 hover:border-primary-60'
                    "
                    @click="selectTab(tab.key)"
                >
                    {{ tab.label }}
                </button>
            </div>

            <div
                v-if="teachers.length"
                class="mt-[40px] grid grid-cols-1 justify-items-center gap-[40px] sm:mt-10 sm:grid-cols-2 sm:gap-6 lg:grid-cols-3"
            >
                <CardDaftarGuru
                    v-for="teacher in teachers"
                    :key="teacher.id"
                    :teacher="teacher"
                />
            </div>
            <p v-else class="mt-10 text-center text-neutral-40">
                Belum ada data.
            </p>

            <nav
                v-if="lastPage > 1"
                aria-label="Navigasi halaman"
                class="mt-[30px] flex items-center justify-center gap-[8px] sm:mt-10 sm:gap-2"
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
