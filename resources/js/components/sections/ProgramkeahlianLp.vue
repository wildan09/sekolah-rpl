<script setup>
import { ref, computed, watch } from "vue";
const tabs = [
    {
        nama: "Semua Jurusan",
        ikon: '<circle cx="12" cy="12" r="10"/><path d="m9 12 2 2 4-4"/>',
    },
    {
        nama: "Teknologi Informasi",
        ikon: '<path d="M15 14c.2-1 .7-1.7 1.5-2.5 1-.9 1.5-2.2 1.5-3.5A6 6 0 0 0 6 8c0 1 .2 2.2 1.5 3.5.7.7 1.3 1.5 1.5 2.5"/><path d="M9 18h6"/><path d="M10 22h4"/>',
    },
    {
        nama: "Teknologi dan Rekayasa",
        ikon: '<rect width="14" height="20" x="5" y="2" rx="2" ry="2"/><path d="M12 18h.01"/>',
    },
    {
        nama: "Agribisnis dan Agroteknologi",
        ikon: '<path d="M2 22 16 8"/><path d="M3.47 12.53 5 11l1.53 1.53a3.5 3.5 0 0 1 0 4.94L5 19l-1.53-1.53a3.5 3.5 0 0 1 0-4.94Z"/><path d="M7.47 8.53 9 7l1.53 1.53a3.5 3.5 0 0 1 0 4.94L9 15l-1.53-1.53a3.5 3.5 0 0 1 0-4.94Z"/><path d="M11.47 4.53 13 3l1.53 1.53a3.5 3.5 0 0 1 0 4.94L13 11l-1.53-1.53a3.5 3.5 0 0 1 0-4.94Z"/>',
    },
    {
        nama: "Teknologi Elektronika",
        ikon: '<circle cx="12" cy="12" r="1"/><path d="M20.2 20.2c2.04-2.03.02-7.36-4.5-11.9-4.54-4.52-9.87-6.54-11.9-4.5-2.04 2.03-.02 7.36 4.5 11.9 4.54 4.52 9.87 6.54 11.9 4.5Z"/><path d="M15.7 15.7c4.52-4.54 6.54-9.87 4.5-11.9-2.03-2.04-7.36-.02-11.9 4.5-4.52 4.54-6.54 9.87-4.5 11.9 2.03 2.04 7.36.02 11.9-4.5Z"/>',
    },
];

const programList = [
    {
        nama: "Rekayasa Perangkat Lunak",
        jurusan: "Teknologi Informasi",
        deskripsi:
            "Mempelajari pengembangan perangkat lunak, web, aplikasi mobile, dan solusi teknologi informasi",
        gambar: "/images/program/rpl.png",
        link: "#",
    },
    {
        nama: "Teknik Komputer dan Jaringan",
        jurusan: "Teknologi Informasi",
        deskripsi:
            "Mempelajari perakitan komputer, jaringan, server, dan keamanan sistem informasi",
        gambar: "/images/program/tkj.jpg",
        link: "#",
    },
    {
        nama: "Teknik Pemesinan",
        jurusan: "Teknologi dan Rekayasa",
        deskripsi:
            "Mempelajari proses permesinan, pengelasan, dan pembuatan komponen dengan mesin perkakas",
        gambar: "/images/program/pemesinan.jpg",
        link: "#",
    },
    {
        nama: "Teknik Kendaraan Ringan",
        jurusan: "Teknologi dan Rekayasa",
        deskripsi:
            "Mempelajari perawatan, perbaikan, dan teknologi kendaraan ringan modern",
        gambar: "/images/program/tkr.jpg",
        link: "#",
    },
    {
        nama: "Agribisnis Tanaman",
        jurusan: "Agribisnis dan Agroteknologi",
        deskripsi:
            "Mempelajari budidaya tanaman, pengelolaan lahan, dan pemasaran hasil pertanian",
        gambar: "/images/program/agribisnis.jpg",
        link: "#",
    },
    {
        nama: "Agroteknologi Pengolahan Hasil",
        jurusan: "Agribisnis dan Agroteknologi",
        deskripsi:
            "Mempelajari pengolahan hasil pertanian menjadi produk bernilai jual tinggi",
        gambar: "/images/program/agroteknologi.jpg",
        link: "#",
    },
    {
        nama: "Teknik Elektronika Industri",
        jurusan: "Teknologi Elektronika",
        deskripsi:
            "Mempelajari rangkaian elektronika, otomasi, PLC, dan sistem kendali industri",
        gambar: "/images/program/elektronika.jpg",
        link: "#",
    },
];
const activeTab = ref("Semua Jurusan");
const index = ref(0);

const filtered = computed(() =>
    activeTab.value === "Semua Jurusan"
        ? programList
        : programList.filter((p) => p.jurusan === activeTab.value),
);

const current = computed(() => filtered.value[index.value] ?? null);

watch(activeTab, () => (index.value = 0));

const prev = () => {
    if (!filtered.value.length) return;
    index.value =
        (index.value - 1 + filtered.value.length) % filtered.value.length;
};
const next = () => {
    if (!filtered.value.length) return;
    index.value = (index.value + 1) % filtered.value.length;
};
const pilihTab = (nama, event) => {
    activeTab.value = nama;
    event.currentTarget.scrollIntoView({
        behavior: "smooth",
        inline: "center",
        block: "nearest",
    });
};
let startX = 0;
let startY = 0;
const onTouchStart = (e) => {
    startX = e.touches[0].clientX;
    startY = e.touches[0].clientY;
};
const onTouchEnd = (e) => {
    const dx = e.changedTouches[0].clientX - startX;
    const dy = e.changedTouches[0].clientY - startY;
    if (Math.abs(dx) > 50 && Math.abs(dx) > Math.abs(dy)) {
        dx > 0 ? prev() : next();
    }
};
</script>

<template>
    <section class="w-full px-4 py-10 sm:px-8 sm:py-14 lg:px-27.5 lg:py-16">
        <div class="mx-auto max-w-[1000px]">
            <div class="text-center">
                <h2
                    class="text-[26px] font-bold leading-[1.2] tracking-[-0.02em] text-[#1F2937] sm:text-[34px] lg:text-[40px]"
                >
                    Program Keahlian
                </h2>
                <p
                    class="mx-auto mt-2 max-w-[580px] text-[13px] leading-relaxed text-[#A3A3A3] sm:text-[15px] lg:text-[16px]"
                >
                    SMK Negeri 1 Purwosari menyediakan 4 program jurusan dan 10
                    konsentrasi keahlian. Mari pilih keahlian yang sesuai dengan
                    minat dan bakatmu.
                </p>
            </div>
            <div
                class="tabs -mx-4 mt-6 flex gap-2 overflow-x-auto px-4 py-2 sm:mx-0 sm:flex-wrap sm:justify-center sm:gap-2.5 sm:overflow-visible sm:px-0"
            >
                <button
                    v-for="tab in tabs"
                    :key="tab.nama"
                    type="button"
                    @click="pilihTab(tab.nama, $event)"
                    :class="
                        activeTab === tab.nama
                            ? 'border-[#FFC107] bg-[#FFC107] text-[#1F2937] shadow-[0_4px_14px_rgba(255,193,7,0.35)]'
                            : 'border-gray-200 bg-white text-[#1F2937] shadow-[0_2px_10px_rgba(0,0,0,0.05)] hover:border-[#FFC107]'
                    "
                    class="inline-flex h-9 shrink-0 items-center gap-1.5 whitespace-nowrap rounded-lg border px-3 text-[11px] font-medium transition-all duration-200 sm:gap-2 sm:px-3.5 sm:text-[12px]"
                >
                    <svg
                        width="15"
                        height="15"
                        viewBox="0 0 24 24"
                        fill="none"
                        stroke="currentColor"
                        stroke-width="1.8"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        class="shrink-0"
                        v-html="tab.ikon"
                    ></svg>
                    {{ tab.nama }}
                </button>
            </div>
            <div
                v-if="current"
                class="relative mt-4 flex items-center sm:mt-8 sm:gap-5 lg:gap-6"
            >
                <button
                    type="button"
                    @click="prev"
                    class="absolute left-2 top-1/2 z-10 flex h-8 w-8 -translate-y-1/2 items-center justify-center rounded-md bg-[#FFC107] text-white shadow-md transition hover:bg-[#e6ad00] sm:static sm:translate-y-0 sm:shadow-none"
                    aria-label="Sebelumnya"
                >
                    <svg width="9" height="16" viewBox="0 0 10 16" fill="none">
                        <path
                            d="M9 1L2 8L9 15"
                            stroke="currentColor"
                            stroke-width="2.2"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                        />
                    </svg>
                </button>
                <div
                    class="relative aspect-[4/3] min-w-0 flex-1 overflow-hidden rounded-2xl bg-[#111827] shadow-[0_8px_30px_rgba(0,0,0,0.18)] sm:aspect-[2/1] sm:rounded-[20px] lg:aspect-[2.5/1]"
                    @touchstart.passive="onTouchStart"
                    @touchend.passive="onTouchEnd"
                >
                    <Transition
                        mode="out-in"
                        enter-active-class="transition duration-500 ease-out"
                        enter-from-class="opacity-0"
                        enter-to-class="opacity-100"
                        leave-active-class="transition duration-200 ease-in"
                        leave-from-class="opacity-100"
                        leave-to-class="opacity-0"
                    >
                        <div
                            :key="activeTab + '-' + index"
                            class="absolute inset-0"
                        >
                            <img
                                :src="current.gambar"
                                :alt="current.nama"
                                class="h-full w-full object-cover"
                            />
                            <div
                                class="absolute inset-0 bg-black/30 backdrop-blur-[2px]"
                            ></div>
                            <div
                                class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/25 to-transparent"
                            ></div>
                            <div
                                class="absolute inset-x-0 bottom-0 p-4 sm:p-6 lg:p-8"
                            >
                                <h3
                                    class="text-[18px] font-bold leading-tight text-white sm:text-[22px] lg:text-[26px]"
                                >
                                    {{ current.nama }}
                                </h3>
                                <p
                                    class="mt-1.5 line-clamp-3 text-[12px] leading-relaxed text-white/70 sm:line-clamp-2 sm:text-[13px] lg:text-[15px]"
                                >
                                    {{ current.deskripsi }}
                                </p>
                                <a
                                    :href="current.link"
                                    class="group mt-3 inline-flex items-center gap-2 text-[12px] font-medium text-[#FFC107] sm:text-[14px]"
                                >
                                    Lihat detail
                                    <svg
                                        width="16"
                                        height="16"
                                        viewBox="0 0 24 24"
                                        fill="none"
                                        stroke="currentColor"
                                        stroke-width="2"
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        class="transition duration-300 group-hover:translate-x-1"
                                    >
                                        <path d="M5 12h14" />
                                        <path d="m13 6 6 6-6 6" />
                                    </svg>
                                </a>
                            </div>
                        </div>
                    </Transition>
                </div>
                <button
                    type="button"
                    @click="next"
                    class="absolute right-2 top-1/2 z-10 flex h-8 w-8 -translate-y-1/2 items-center justify-center rounded-md bg-[#FFC107] text-white shadow-md transition hover:bg-[#e6ad00] sm:static sm:translate-y-0 sm:shadow-none"
                    aria-label="Berikutnya"
                >
                    <svg width="9" height="16" viewBox="0 0 10 16" fill="none">
                        <path
                            d="M1 1L8 8L1 15"
                            stroke="currentColor"
                            stroke-width="2.2"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                        />
                    </svg>
                </button>
            </div>
            <p v-else class="mt-10 text-center text-[14px] text-[#A3A3A3]">
                Belum ada program untuk jurusan ini.
            </p>
            <div
                v-if="filtered.length > 1"
                class="mt-4 flex items-center justify-center gap-1.5"
            >
                <button
                    v-for="(_, i) in filtered"
                    :key="i"
                    type="button"
                    @click="index = i"
                    :class="
                        index === i ? 'w-6 bg-[#FFC107]' : 'w-1.5 bg-[#D4D4D4]'
                    "
                    class="h-1.5 rounded-full transition-all duration-300"
                    :aria-label="'Program ' + (i + 1)"
                ></button>
            </div>
        </div>
    </section>
</template>

<style scoped>
.tabs {
    scrollbar-width: none;
}
.tabs::-webkit-scrollbar {
    display: none;
}
</style>
