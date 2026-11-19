<script setup>
import {
    ref,
    computed,
    watch,
    nextTick,
    onMounted,
    onBeforeUnmount,
} from "vue";
const currentPage = ref(1);
const itemsPerPage = 6;

const ekstrakurikulerList = [
    {
        nama: "Prakarsa",
        deskripsi:
            "Prakarsa merupakan ambalan Pramuka SMKN 1 Purwosari, terdiri dari Untung Suropati dan R.A. Kartini.",
        gambar: "/images/ekstrakurikuler/prakarsa.jpg",
        logo: "/images/ekstrakurikuler/logo-prakarsa.png",
        paragraf:
            'Prakarsa adalah akronim dari Pramuka SMKN 1 Purwosari dengan nama ambalan Untung Suropati dan R.A.Kartini. Prakarsa memiliki nomor gudep 14.147 dan 14.148 dengan satu sanggar yang diberi nama "Sanggar Bhakti". Adapun kepengurusan dalam Prakarsa sendiri bernama Dewan Ambalan yang dipimpin oleh seorang pradana. Prakarsa sendiri memiliki 2 pembina yaitu Pembina dalam (Kak Amin) dan Pembina luar (Kak Faruk).',
        kegiatanIntro:
            "Seluruh kegiatan yang diselenggarakan di Prakarsa selalu mematuhi AD & ART serta Tata Tertib SMKN 1 Purwosari. Metode Pelaksaan kegiatan dibagi menjadi 3, yaitu :",
        kegiatan: [
            "Metode Blok Bersifat wajib, dilaksanakan setahun sekali dan berlaku bagi seluruh peserta didik. Salah satu kegiatan kami yang menggunakan metode ini adalah CARAKA (Calon Anggota Pramuka). Caraka yaitu salah satu program tahunan yang rutin dilaksanakan sebagai penutup MPLS dengan Persami. Hal ini ditujukan sebagai penyambutan peserta didik baru sekaligus penanda naiknya tingkatan dari pramuka penggalang menuju pramuka penegak.",
            "Metode Aktualisasi Bersifat wajib, rutin dan berlaku untuk seluruh peserta didik dengan penjadwalan serta terdapat penilaian secara formal. Salah satu kegiatan kami yang menggunakan metode ini adalah ekstra wajib. Ekstra wajib sendiri dilaksanakan setiap hari Sabtu sepulang sekolah dengan bergilir 4 kelas setiap minggunya.",
            "Reguler Bersifat sukarela dan berbasis minat. Seluruh kegiatan dalam ekstra regular diatur oleh program kerja yang telah disusun oleh Dewan Ambalan dan telah mendapat persetujuan dari seluruh anggota. Program kerja tersebut terdiri dari proker mingguan, bulanan dan tahunan. Salah satu cirri khas program kerja tahunan kami adalah FESTIVAL PRAKARSA. Tahun ini festival tersebut dilaksanakan pada tanggal 7-8 Februari 2020 dengan kegiatan meliputi : reboisasi, biopori dan festival kecerdasan.",
        ],
        sosmed: {
            username: "@pramuka_smknpur",
            url: "https://instagram.com/pramuka_smknpur",
        },
        dokumentasi: [
            "/images/ekstrakurikuler/dok/prakarsa-1.jpg",
            "/images/ekstrakurikuler/dok/prakarsa-2.jpg",
            "/images/ekstrakurikuler/dok/prakarsa-3.jpg",
            "/images/ekstrakurikuler/dok/prakarsa-4.jpg",
            "/images/ekstrakurikuler/dok/prakarsa-5.jpg",
            "/images/ekstrakurikuler/dok/prakarsa-6.jpg",
            "/images/ekstrakurikuler/dok/prakarsa-7.jpg",
            "/images/ekstrakurikuler/dok/prakarsa-8.jpg",
        ],
    },
    {
        nama: "Paskanusa",
        deskripsi:
            "PASKANUSA merupakan ekstrakurikuler Paskibra SMKN 1 Purwosari yang berdiri sejak 18 Oktober 2002.",
        gambar: "/images/ekstrakurikuler/paskanusa.jpg",
        logo: "/images/ekstrakurikuler/logo-paskanusa.png",
        paragraf: "",
        kegiatanIntro: "",
        kegiatan: [],
        sosmed: null,
        dokumentasi: [],
    },
    {
        nama: "PMR",
        deskripsi:
            "PMR merupakan ekstrakurikuler yang berfokus pada pertolongan pertama, kesehatan, donor darah, dan kemanusiaan.",
        gambar: "/images/ekstrakurikuler/pmr.jpg",
        logo: "/images/ekstrakurikuler/logo-pmr.png",
        paragraf: "",
        kegiatanIntro: "",
        kegiatan: [],
        sosmed: null,
        dokumentasi: [],
    },
    {
        nama: "Broadcasting",
        deskripsi:
            "X-Gen Broadcasting (BC) adalah ekstrakurikuler videografi, presenter, karya visual di SMKN 1 Purwosari.",
        gambar: "/images/ekstrakurikuler/broadcasting.jpg",
        logo: "/images/ekstrakurikuler/logo-broadcasting.png",
        paragraf: "",
        kegiatanIntro: "",
        kegiatan: [],
        sosmed: null,
        dokumentasi: [],
    },
    {
        nama: "MCC",
        deskripsi:
            "Metamorph Creative Crew (MCC) merupakan ekstrakurikuler jurnalistik di bidang fotografi, desain, dan dokumentasi.",
        gambar: "/images/ekstrakurikuler/mcc.jpg",
        logo: "/images/ekstrakurikuler/logo-mcc.png",
        paragraf: "",
        kegiatanIntro: "",
        kegiatan: [],
        sosmed: null,
        dokumentasi: [],
    },
    {
        nama: "Pecinta Alam",
        deskripsi:
            "Yang biasa dikenal dengan Degdayapala, berfokus pada kegiatan alam bebas, wall climbing, dan kepedulian lingkungan, dls.",
        gambar: "/images/ekstrakurikuler/pecinta-alam.jpg",
        logo: "/images/ekstrakurikuler/logo-pecinta-alam.png",
        paragraf: "",
        kegiatanIntro: "",
        kegiatan: [],
        sosmed: null,
        dokumentasi: [],
    },
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
const modalOpen = ref(false);
const selected = ref(null);
const scrollArea = ref(null);
const gallery = ref(null);

const docSlide = ref(0);
const perView = ref(4);
const docSlideCount = computed(() => {
    if (!selected.value) return 0;
    return Math.ceil(selected.value.dokumentasi.length / perView.value);
});

const onGalleryScroll = () => {
    const el = gallery.value;
    if (!el) return;

    const max = el.scrollWidth - el.clientWidth;
    if (max <= 0 || docSlideCount.value <= 1) {
        docSlide.value = 0;
        return;
    }

    docSlide.value = Math.round(
        (el.scrollLeft / max) * (docSlideCount.value - 1),
    );
};

const updatePerView = () => {
    perView.value = window.matchMedia("(min-width: 640px)").matches ? 4 : 2;
    onGalleryScroll();
};

const goToDocSlide = (index) => {
    const el = gallery.value;
    if (!el) return;

    const i = Math.min(Math.max(index, 0), docSlideCount.value - 1);
    const target = el.children[i * perView.value];

    if (target) {
        el.scrollTo({ left: target.offsetLeft, behavior: "smooth" });
    }
};

const openModal = async (item) => {
    selected.value = item;
    docSlide.value = 0;
    modalOpen.value = true;

    await nextTick();
    if (scrollArea.value) scrollArea.value.scrollTop = 0;
    if (gallery.value) gallery.value.scrollLeft = 0;
};

const closeModal = () => {
    modalOpen.value = false;
};

watch(modalOpen, (isOpen) => {
    document.body.style.overflow = isOpen ? "hidden" : "";
});

const handleKeydown = (event) => {
    if (!modalOpen.value) return;
    if (event.key === "Escape") closeModal();
    if (event.key === "ArrowLeft") goToDocSlide(docSlide.value - 1);
    if (event.key === "ArrowRight") goToDocSlide(docSlide.value + 1);
};

onMounted(() => {
    updatePerView();
    window.addEventListener("keydown", handleKeydown);
    window.addEventListener("resize", updatePerView);
});

onBeforeUnmount(() => {
    window.removeEventListener("keydown", handleKeydown);
    window.removeEventListener("resize", updatePerView);
    document.body.style.overflow = "";
});
</script>

<template>
    <section class="w-full px-4 py-10 sm:px-8 sm:py-14 lg:px-27.5">
        <div class="flex flex-col items-center text-center">
            <div class="mb-2 flex items-center gap-2">
                <span class="text-[#FFC107]">
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
                <span
                    class="text-[14px] font-bold uppercase tracking-wide text-[#1F2937] sm:text-[16px]"
                >
                    Ekstrakurikuler
                </span>
            </div>

            <h2
                class="max-w-[600px] text-[26px] font-bold leading-[1.2] tracking-[-0.02em] text-[#1F2937] sm:text-[34px] lg:text-[40px]"
            >
                Kembangkan Bakat, Raih Prestasi Bersama Ekstrakurikuler
            </h2>
        </div>
        <div
            class="mx-auto mt-8 grid max-w-[800px] grid-cols-1 gap-4 sm:mt-10 sm:grid-cols-2 sm:gap-5 lg:grid-cols-3 lg:gap-6"
        >
            <button
                v-for="item in paginatedEkstrakurikuler"
                :key="item.nama"
                type="button"
                @click="openModal(item)"
                class="group flex cursor-pointer flex-col overflow-hidden rounded-[10px] bg-white text-left shadow-[0_2px_12px_rgba(0,0,0,0.06)] transition duration-300 hover:-translate-y-1 hover:shadow-[0_8px_24px_rgba(0,0,0,0.10)] focus:outline-none focus-visible:ring-2 focus-visible:ring-[#FFD000]"
            >
                <div class="aspect-[1.92/1] w-full overflow-hidden bg-gray-100">
                    <img
                        :src="item.gambar"
                        :alt="item.nama"
                        loading="lazy"
                        class="h-full w-full object-cover transition duration-500 group-hover:scale-105"
                    />
                </div>
                <div class="flex flex-1 flex-col px-4 pb-4 pt-3">
                    <div class="flex items-center justify-between gap-3">
                        <div class="flex min-w-0 items-center gap-3">
                            <span
                                class="flex h-9 w-9 shrink-0 items-center justify-center overflow-hidden rounded-full bg-white shadow-[0_1px_6px_rgba(0,0,0,0.12)]"
                            >
                                <img
                                    :src="item.logo"
                                    :alt="'Logo ' + item.nama"
                                    class="h-full w-full object-contain"
                                />
                            </span>
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
                        class="mt-3 line-clamp-3 text-[11px] leading-[1.6] text-[#A3A3A3]"
                    >
                        {{ item.deskripsi }}
                    </p>
                </div>
            </button>
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

                <template v-for="(page, index) in paginationPages" :key="index">
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
    </section>
    <Teleport to="body">
        <Transition
            enter-active-class="transition duration-300 ease-out"
            enter-from-class="opacity-0"
            enter-to-class="opacity-100"
            leave-active-class="transition duration-200 ease-in"
            leave-from-class="opacity-100"
            leave-to-class="opacity-0"
        >
            <div
                v-if="modalOpen && selected"
                class="fixed inset-0 z-[9999] flex items-center justify-center p-3 sm:p-6"
            >
                <div
                    class="absolute inset-0 bg-black/60"
                    @click="closeModal"
                ></div>

                <div
                    class="relative flex max-h-[92vh] w-full max-w-[640px] flex-col overflow-hidden rounded-[20px] bg-white shadow-2xl"
                    role="dialog"
                    aria-modal="true"
                    :aria-label="selected.nama"
                >
                    <div
                        class="flex items-center justify-between gap-3 px-5 pb-3 pt-5 sm:px-8 sm:pt-6"
                    >
                        <div class="flex min-w-0 items-center gap-3">
                            <span
                                class="flex h-11 w-11 shrink-0 items-center justify-center overflow-hidden rounded-full bg-white shadow-[0_1px_6px_rgba(0,0,0,0.12)] sm:h-12 sm:w-12"
                            >
                                <img
                                    :src="selected.logo"
                                    :alt="'Logo ' + selected.nama"
                                    class="h-full w-full object-contain"
                                />
                            </span>
                            <h3
                                class="truncate text-[20px] font-bold uppercase text-[#1F2937] sm:text-[24px]"
                            >
                                {{ selected.nama }}
                            </h3>
                        </div>

                        <button
                            type="button"
                            @click="closeModal"
                            class="flex h-9 w-9 shrink-0 items-center justify-center rounded-full text-[#1F2937] transition hover:bg-gray-100"
                            aria-label="Tutup"
                        >
                            <svg
                                width="20"
                                height="20"
                                viewBox="0 0 24 24"
                                xmlns="http://www.w3.org/2000/svg"
                            >
                                <path
                                    fill="none"
                                    stroke="currentColor"
                                    stroke-width="1.6"
                                    stroke-linecap="round"
                                    d="m6 6l12 12m0-12L6 18"
                                />
                            </svg>
                        </button>
                    </div>
                    <div
                        ref="scrollArea"
                        class="modal-scroll flex-1 overflow-y-auto pl-5 pr-4 pb-4 sm:pl-8 sm:pr-6"
                    >
                        <p
                            v-if="selected.paragraf"
                            class="indent-8 text-justify text-[12px] leading-[1.7] text-[#8C8C8C] sm:text-[13px]"
                        >
                            {{ selected.paragraf }}
                        </p>

                        <div v-if="selected.kegiatanIntro" class="mt-5">
                            <p
                                class="text-[12px] font-medium leading-[1.7] text-[#8C8C8C] sm:text-[13px]"
                            >
                                KEGIATAN:
                            </p>
                            <p
                                class="text-justify text-[12px] leading-[1.7] text-[#8C8C8C] sm:text-[13px]"
                            >
                                {{ selected.kegiatanIntro }}
                            </p>

                            <ol
                                class="mt-1 ml-5 list-decimal space-y-1.5 text-justify text-[12px] leading-[1.7] text-[#8C8C8C] marker:text-[#8C8C8C] sm:text-[13px]"
                            >
                                <li
                                    v-for="(kegiatan, i) in selected.kegiatan"
                                    :key="i"
                                    class="pl-1"
                                >
                                    {{ kegiatan }}
                                </li>
                            </ol>
                        </div>
                        <p
                            v-if="!selected.paragraf && !selected.kegiatanIntro"
                            class="text-justify text-[12px] leading-[1.7] text-[#8C8C8C] sm:text-[13px]"
                        >
                            {{ selected.deskripsi }}
                        </p>
                        <div
                            v-if="selected.sosmed"
                            class="mt-8 text-center sm:mt-10"
                        >
                            <h4
                                class="text-[15px] font-bold text-[#1F2937] sm:text-[16px]"
                            >
                                Sosial Media
                            </h4>
                            <a
                                :href="selected.sosmed.url"
                                target="_blank"
                                rel="noopener"
                                class="mt-1.5 inline-flex items-center gap-2 text-[13px] text-[#1F2937] hover:underline"
                            >
                                <svg
                                    width="20"
                                    height="20"
                                    viewBox="0 0 24 24"
                                    xmlns="http://www.w3.org/2000/svg"
                                >
                                    <defs>
                                        <linearGradient
                                            id="ig-grad"
                                            x1="0"
                                            y1="1"
                                            x2="1"
                                            y2="0"
                                        >
                                            <stop
                                                offset="0"
                                                stop-color="#FEDA75"
                                            />
                                            <stop
                                                offset="0.35"
                                                stop-color="#FA7E1E"
                                            />
                                            <stop
                                                offset="0.6"
                                                stop-color="#D62976"
                                            />
                                            <stop
                                                offset="0.8"
                                                stop-color="#962FBF"
                                            />
                                            <stop
                                                offset="1"
                                                stop-color="#4F5BD5"
                                            />
                                        </linearGradient>
                                    </defs>
                                    <rect
                                        width="24"
                                        height="24"
                                        rx="6"
                                        fill="url(#ig-grad)"
                                    />
                                    <rect
                                        x="5"
                                        y="5"
                                        width="14"
                                        height="14"
                                        rx="4"
                                        fill="none"
                                        stroke="white"
                                        stroke-width="1.6"
                                    />
                                    <circle
                                        cx="12"
                                        cy="12"
                                        r="3.2"
                                        fill="none"
                                        stroke="white"
                                        stroke-width="1.6"
                                    />
                                    <circle
                                        cx="16.2"
                                        cy="7.8"
                                        r="1"
                                        fill="white"
                                    />
                                </svg>
                                {{ selected.sosmed.username }}
                            </a>
                            <p class="mt-1 text-[11px] text-[#A3A3A3]">
                                Ikuti aktivitas dan informasi terbaru kami
                                melalui media sosial.
                            </p>
                        </div>
                        <div
                            v-if="selected.dokumentasi.length"
                            class="mt-8 sm:mt-10"
                        >
                            <h4
                                class="text-[18px] font-bold text-[#1F2937] sm:text-[22px]"
                            >
                                Dokumentasi Kegiatan
                            </h4>

                            <div
                                ref="gallery"
                                @scroll.passive="onGalleryScroll"
                                class="gallery relative mt-4 flex snap-x snap-mandatory gap-2.5 overflow-x-auto scroll-smooth sm:gap-3"
                            >
                                <div
                                    v-for="(foto, i) in selected.dokumentasi"
                                    :key="i"
                                    class="aspect-[1.45/1] w-[calc((100%-0.625rem)/2)] shrink-0 snap-start overflow-hidden rounded-lg bg-gray-100 sm:w-[calc((100%-2.25rem)/4)]"
                                >
                                    <img
                                        :src="foto"
                                        :alt="'Dokumentasi ' + selected.nama"
                                        loading="lazy"
                                        class="h-full w-full object-cover"
                                    />
                                </div>
                            </div>
                        </div>
                    </div>
                    <div
                        v-if="docSlideCount > 1"
                        class="flex items-center justify-center gap-1 pb-4 pt-2"
                    >
                        <button
                            v-for="(_, i) in docSlideCount"
                            :key="i"
                            type="button"
                            @click="goToDocSlide(i)"
                            :class="
                                docSlide === i
                                    ? 'w-[86px] bg-[#FFC800]'
                                    : 'w-1.5 bg-[#D4D4D4]'
                            "
                            class="h-1 rounded-full transition-all duration-300"
                            :aria-label="'Halaman dokumentasi ' + (i + 1)"
                        ></button>
                    </div>
                    <div v-else class="pb-3"></div>
                </div>
            </div>
        </Transition>
    </Teleport>
</template>

<style scoped>
.modal-scroll {
    scrollbar-width: thin;
    scrollbar-color: #ffc800 #e5e5e5;
}
.modal-scroll::-webkit-scrollbar {
    width: 6px;
}
.modal-scroll::-webkit-scrollbar-track {
    background: #e5e5e5;
    border-radius: 9999px;
}
.modal-scroll::-webkit-scrollbar-thumb {
    background: #ffc800;
    border-radius: 9999px;
}

/* Sembunyikan scrollbar galeri, dot jadi indikatornya */
.gallery {
    scrollbar-width: none;
}
.gallery::-webkit-scrollbar {
    display: none;
}
</style>
