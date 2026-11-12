<script setup>
import { ref, computed } from "vue";

const selectedJurusan = ref("Semua Prodi");

const currentPage = ref(1);

const itemsPerPage = 9;

const jurusanList = [
    "Semua Prodi",
    "Teknik Informatika",
    "Teknologi & Rekayasa",
    "Agribisnis dan Agroteknologi",
    "Teknologi Elektronika",
];

const fasilitasList = [
    {
        nama: "Komputer",
        jurusan: "Teknik Informatika",
        warna: "#FFD45C",
        gambar: "/images/fasilitas/image.png",
    },
    {
        nama: "Mesin Frais",
        jurusan: "Teknologi & Rekayasa",
        warna: "#FFD45C",
        gambar: "/images/fasilitas/mesin-frais.jpg",
    },
    {
        nama: "Laboratorium Pertanian",
        jurusan: "Agribisnis dan Agroteknologi",
        warna: "#FFD45C",
        gambar: "/images/fasilitas/laboratorium-pertanian.jpg",
    },
    {
        nama: "Pneumatic dan elektronik",
        jurusan: "Teknologi Elektronika",
        warna: "#FFD45C",
        gambar: "/images/fasilitas/pneumatic.jpg",
    },
    {
        nama: "Tanaman & Hortikultura",
        jurusan: "Agribisnis dan Agroteknologi",
        warna: "#3B82F6",
        gambar: "/images/fasilitas/tanaman.jpg",
    },
    {
        nama: "Laser Cutting",
        jurusan: "Teknologi & Rekayasa",
        warna: "#3B82F6",
        gambar: "/images/fasilitas/laser-cutting.jpg",
    },
    {
        nama: "Plasma Cutting",
        jurusan: "Teknologi & Rekayasa",
        warna: "#3B82F6",
        gambar: "/images/fasilitas/plasma-cutting.jpg",
    },
    {
        nama: "CNC Milling",
        jurusan: "Teknologi & Rekayasa",
        warna: "#3B82F6",
        gambar: "/images/fasilitas/cnc-milling.jpg",
    },
    {
        nama: "CNC Turning",
        jurusan: "Teknologi & Rekayasa",
        warna: "#3B82F6",
        gambar: "/images/fasilitas/cnc-turning.jpg",
    },
    {
        nama: "Laboratorium Jaringan",
        jurusan: "Teknik Informatika",
        warna: "#FFD45C",
        gambar: "/images/fasilitas/lab-jaringan.jpg",
    },
    {
        nama: "Laboratorium Pemrograman",
        jurusan: "Teknik Informatika",
        warna: "#FFD45C",
        gambar: "/images/fasilitas/lab-pemrograman.jpg",
    },
    {
        nama: "Studio Multimedia",
        jurusan: "Teknik Informatika",
        warna: "#FFD45C",
        gambar: "/images/fasilitas/studio-multimedia.jpg",
    },
    {
        nama: "Bengkel Otomotif",
        jurusan: "Teknologi & Rekayasa",
        warna: "#3B82F6",
        gambar: "/images/fasilitas/bengkel-otomotif.jpg",
    },
    {
        nama: "Workshop Las",
        jurusan: "Teknologi & Rekayasa",
        warna: "#3B82F6",
        gambar: "/images/fasilitas/workshop-las.jpg",
    },
    {
        nama: "Laboratorium Hidroponik",
        jurusan: "Agribisnis dan Agroteknologi",
        warna: "#3B82F6",
        gambar: "/images/fasilitas/lab-hidroponik.jpg",
    },
    {
        nama: "Greenhouse",
        jurusan: "Agribisnis dan Agroteknologi",
        warna: "#3B82F6",
        gambar: "/images/fasilitas/greenhouse.jpg",
    },
    {
        nama: "Laboratorium Elektronika",
        jurusan: "Teknologi Elektronika",
        warna: "#3B82F6",
        gambar: "/images/fasilitas/lab-elektronika.jpg",
    },
    {
        nama: "Workshop Elektronika",
        jurusan: "Teknologi Elektronika",
        warna: "#3B82F6",
        gambar: "/images/fasilitas/workshop-elektronika.jpg",
    },
    {
        nama: "Laboratorium PLC",
        jurusan: "Teknologi Elektronika",
        warna: "#3B82F6",
        gambar: "/images/fasilitas/lab-plc.jpg",
    },
    {
        nama: "Ruang Praktik Desain",
        jurusan: "Teknik Informatika",
        warna: "#FFD45C",
        gambar: "/images/fasilitas/ruang-desain.jpg",
    },
];

const filteredFasilitas = computed(() => {
    if (selectedJurusan.value === "Semua Prodi") {
        return fasilitasList;
    }

    return fasilitasList.filter(
        (item) => item.jurusan === selectedJurusan.value,
    );
});

const totalPages = computed(() => {
    return Math.ceil(filteredFasilitas.value.length / itemsPerPage);
});

const paginatedFasilitas = computed(() => {
    const start = (currentPage.value - 1) * itemsPerPage;
    const end = start + itemsPerPage;

    return filteredFasilitas.value.slice(start, end);
});

const goToPage = (page) => {
    currentPage.value = page;
};

const previousPage = () => {
    if (currentPage.value > 1) {
        currentPage.value--;
    }
};

const nextPage = () => {
    if (currentPage.value < totalPages.value) {
        currentPage.value++;
    }
};

const changeJurusan = () => {
    currentPage.value = 1;
};

const openModal = (index) => {
    const images = paginatedFasilitas.value.map((item) => ({
        nama: item.nama,
        gambar: item.gambar,
    }));

    window.dispatchEvent(
        new CustomEvent("open-fasilitas-modal", {
            detail: {
                images: images,
                index: index,
            },
        }),
    );
};
</script>
<template>
    <section class="w-full px-27.5 py-6">
        <div class="flex items-end justify-between gap-6">
            <div>
                <div class="mb-2 flex items-center gap-2">
                    <span
                        class="flex h-5 w-5 items-center justify-center text-[#FFD45C]"
                    >
                        <svg
                            width="45"
                            height="31"
                            viewBox="0 0 45 31"
                            fill="none"
                            xmlns="http://www.w3.org/2000/svg"
                        >
                            <path
                                d="M44.6997 10.5297L40.2138 1.55432C40.0485 1.22397 39.8198 0.929407 39.5407 0.687454C39.2616 0.445502 38.9376 0.260899 38.5871 0.144188C38.2366 0.0274775 37.8666 -0.0190551 37.4982 0.00724798C37.1297 0.033551 36.7701 0.132175 36.4398 0.297486L32.0681 2.48245L22.8589 0.0461192C22.6226 -0.0153731 22.3745 -0.0153731 22.1382 0.0461192L12.929 2.48245L8.55734 0.297486C8.22701 0.132175 7.86736 0.033551 7.49892 0.00724798C7.13047 -0.0190551 6.76046 0.0274775 6.41 0.144188C6.05954 0.260899 5.7355 0.445502 5.4564 0.687454C5.17729 0.929407 4.94857 1.22397 4.78332 1.55432L0.297378 10.528C0.132066 10.8583 0.0334429 11.2179 0.00713983 11.5864C-0.0191632 11.9548 0.0273693 12.3248 0.14408 12.6753C0.260791 13.0258 0.445393 13.3498 0.687346 13.6289C0.929299 13.908 1.22386 14.1367 1.55421 14.302L6.30031 16.6768L16.0544 23.643C16.1981 23.7453 16.3597 23.8198 16.5308 23.8627L27.7808 26.6752C28.0164 26.7343 28.2633 26.7314 28.4974 26.6667C28.7315 26.602 28.9449 26.4777 29.1167 26.3061L38.797 16.624L43.4411 14.302C44.1078 13.9682 44.6148 13.3834 44.8504 12.676C45.0861 11.9687 45.0313 11.1967 44.698 10.5297H44.6997ZM35.0511 16.3955L29.0025 11.551C28.7315 11.334 28.3898 11.2249 28.0432 11.2447C27.6966 11.2645 27.3696 11.4118 27.1251 11.6582C23.9945 14.8117 20.5052 14.4127 18.2798 13.0065L25.8806 5.62366H31.4722L36.2552 15.1879L35.0511 16.3955ZM7.29875 2.81116L10.897 4.60764L6.40226 13.5813L2.81105 11.7865L7.29875 2.81116ZM27.6894 23.752L17.4747 21.1996L8.82629 15.0227L13.7482 5.17893L22.4986 2.86038L24.2212 3.31565L16.3111 10.9938L16.297 11.0096C15.9992 11.3074 15.7721 11.6682 15.6324 12.0654C15.4928 12.4627 15.4441 12.8863 15.49 13.3048C15.5359 13.7234 15.6752 14.1264 15.8976 14.4839C16.12 14.8415 16.4199 15.1446 16.7751 15.3707C20.3892 17.6787 24.7503 17.3043 28.1851 14.4918L33.0454 18.3959L27.6894 23.752ZM38.5878 13.5795L34.1019 4.61467L37.6984 2.81116L42.1861 11.7865L38.5878 13.5795ZM23.163 29.8692C23.087 30.1731 22.9117 30.443 22.6649 30.6359C22.4182 30.8289 22.114 30.934 21.8007 30.9344C21.6852 30.9342 21.5701 30.9201 21.4579 30.8922L14.1331 29.0606C13.9618 29.0183 13.8001 28.9437 13.6568 28.8408L9.02492 25.5326C8.74012 25.309 8.55255 24.9842 8.50127 24.6257C8.44999 24.2673 8.53895 23.9029 8.74963 23.6084C8.96031 23.3139 9.27646 23.112 9.63226 23.0448C9.98806 22.9776 10.3561 23.0502 10.6597 23.2475L15.0736 26.401L22.147 28.1658C22.5087 28.2563 22.8197 28.4868 23.0116 28.8065C23.2034 29.1263 23.2604 29.5092 23.17 29.8709L23.163 29.8692Z"
                                fill="#FFC107"
                            />
                        </svg>
                    </span>

                    <span class="text-[24px] font-Bold uppercase text-[#1F2937]">
                        Fasilitas
                    </span>
                </div>

                <h2
                    class="max-w-158.25 text-[48px] font-bold leading-[1.2] tracking-[-0.02em] text-[#1F2937]"
                >
                    Ruang Belajar yang Mendukung Potensi Setiap Jurusan
                </h2>
            </div>
            <div class="relative w-35 shrink-0">
                <select
                    v-model="selectedJurusan"
                    @change="changeJurusan"
                    class="h-10 w-full appearance-none rounded-lg border border-gray-200 bg-white px-3 pr-9 text-xs text-[#A3A3A3] outline-none transition focus:border-[#FFD45C]"
                >
                    <option
                        v-for="jurusan in jurusanList"
                        :key="jurusan"
                        :value="jurusan"
                    >
                        {{ jurusan }}
                    </option>
                </select>

                <span
                    class="pointer-events-none absolute right-3 top-1/2 -translate-y-1/2 text-gray-400"
                >
                    <svg
                        width="21"
                        height="11"
                        viewBox="0 0 21 11"
                        fill="none"
                        xmlns="http://www.w3.org/2000/svg"
                    >
                        <path
                            d="M0.274717 1.55575L9.65959 10.664C9.74675 10.7487 9.85026 10.8159 9.96419 10.8617C10.0781 10.9076 10.2002 10.9312 10.3236 10.9312C10.4469 10.9312 10.569 10.9076 10.683 10.8617C10.7969 10.8159 10.9004 10.7487 10.9876 10.664L20.3724 1.55575C20.5485 1.38484 20.6475 1.15304 20.6475 0.911336C20.6475 0.669634 20.5485 0.437832 20.3724 0.266924C20.1963 0.0960149 19.9575 0 19.7085 0C19.4594 0 19.2206 0.0960149 19.0445 0.266924L10.3236 8.73194L1.60268 0.266924C1.51548 0.182298 1.41197 0.11517 1.29804 0.0693709C1.18411 0.023572 1.06201 0 0.938698 0C0.815386 0 0.693279 0.023572 0.579353 0.0693709C0.465427 0.11517 0.361912 0.182298 0.274717 0.266924C0.187523 0.351549 0.118357 0.452014 0.071167 0.562582C0.0239773 0.673151 -0.000312805 0.791657 -0.000312805 0.911336C-0.000312805 1.03101 0.0239773 1.14952 0.071167 1.26009C0.118357 1.37066 0.187523 1.47112 0.274717 1.55575Z"
                            fill="#AAAAAA"
                        />
                    </svg>
                </span>
            </div>
        </div>
        <div class="mt-6 flex flex-wrap justify-center gap-6.75">
            <article
                v-for="(fasilitas, index) in paginatedFasilitas"
                :key="fasilitas.nama"
                class="h-67.25 w-[388.67px] shrink-0 overflow-hidden rounded-[10px] bg-white shadow-[0_2px_12px_rgba(0,0,0,0.06)]"
            >
                <button
                    type="button"
                    class="group relative block h-54.75 w-full overflow-hidden text-left"
                    @click="openModal(index)"
                >
                    <img
                        :src="fasilitas.gambar"
                        :alt="fasilitas.nama"
                        class="h-full w-full object-cover transition duration-500 group-hover:scale-105"
                    />
                    <span
                        class="absolute left-2 top-2 inline-flex max-w-[calc(100%-16px)] items-center gap-1 rounded-md bg-white px-2 py-1 text-[10px] font-medium text-[#1F2937] shadow-sm"
                    >
                        <span
                            class="h-1.5 w-1.5 shrink-0 rounded-full"
                            :style="{
                                backgroundColor: fasilitas.warna,
                            }"
                        ></span>

                        <span class="truncate">
                            {{ fasilitas.jurusan }}
                        </span>
                    </span>
                </button>
                <div class="flex h-12.5 items-center px-3">
                    <h3 class="text-sm font-semibold text-[#1F2937]">
                        {{ fasilitas.nama }}
                    </h3>
                </div>
            </article>
        </div>
        <div v-if="totalPages > 1" class="mt-5 flex justify-center">
            <div class="flex items-center gap-1">
                <button
                    type="button"
                    @click="previousPage"
                    :disabled="currentPage === 1"
                    class="flex h-7 w-7 items-center justify-center rounded border border-gray-200 text-xs text-gray-400 transition hover:bg-gray-50 disabled:cursor-not-allowed disabled:opacity-50"
                >
                    ‹
                </button>
                <button
                    v-for="(page, index) in totalPages"
                    :key="index"
                    type="button"
                    @click="goToPage(page)"
                    :class="[
                        'flex h-7 w-7 items-center justify-center rounded border text-xs transition',
                        currentPage === page
                            ? 'border-[#FFD45C] text-[#FFD45C]'
                            : 'border-gray-200 text-gray-500 hover:bg-gray-50',
                    ]"
                >
                    {{ page }}
                </button>
                <button
                    type="button"
                    @click="nextPage"
                    :disabled="currentPage === totalPages"
                    class="flex h-7 w-7 items-center justify-center rounded border border-gray-200 text-xs text-gray-400 transition hover:bg-gray-50 disabled:cursor-not-allowed disabled:opacity-50"
                >
                    <svg
                        width="11"
                        height="21"
                        viewBox="0 0 11 21"
                        fill="none"
                        xmlns="http://www.w3.org/2000/svg"
                    >
                        <path
                            d="M9.37589 0.275208L0.267602 9.66008C0.182916 9.74724 0.115734 9.85075 0.0698967 9.96468C0.0240602 10.0786 0.000469208 10.2007 0.000469208 10.3241C0.000469208 10.4474 0.0240602 10.5695 0.0698967 10.6834C0.115734 10.7974 0.182916 10.9009 0.267602 10.988L9.37589 20.3729C9.5468 20.549 9.7786 20.6479 10.0203 20.6479C10.262 20.6479 10.4938 20.549 10.6647 20.3729C10.8356 20.1968 10.9316 19.958 10.9316 19.7089C10.9316 19.4599 10.8356 19.2211 10.6647 19.045L2.1997 10.3241L10.6647 1.60317C10.7493 1.51597 10.8165 1.41246 10.8623 1.29853C10.9081 1.1846 10.9316 1.0625 10.9316 0.939188C10.9316 0.815874 10.9081 0.693769 10.8623 0.579844C10.8165 0.465918 10.7493 0.362402 10.6647 0.275208C10.5801 0.188011 10.4796 0.118845 10.3691 0.0716553C10.2585 0.0244656 10.14 0.000177383 10.0203 0.000177383C9.90063 0.000177383 9.78212 0.0244656 9.67155 0.0716553C9.56098 0.118845 9.46052 0.188011 9.37589 0.275208Z"
                            fill="white"
                        />
                    </svg>
                </button>
            </div>
        </div>
    </section>
    <div
        x-data="{
        open: false,
        images: [],
        active: 0,
        activeImage: null,

        show(data) {
            this.images = data.images || [];
            this.active = data.index || 0;
            this.activeImage = this.images[this.active] || null;
            this.open = true;

            document.body.style.overflow = 'hidden';

            console.log('Images:', this.images);
            console.log('Active:', this.active);
            console.log('Active Image:', this.activeImage);
        },

        close() {
            this.open = false;
            this.images = [];
            this.active = 0;
            this.activeImage = null;

            document.body.style.overflow = '';
        },

        previous() {
            if (this.active > 0) {
                this.active--;
                this.activeImage = this.images[this.active];
            }
        },

        next() {
            if (this.active < this.images.length - 1) {
                this.active++;
                this.activeImage = this.images[this.active];
            }
        },

        goTo(index) {
            if (index >= 0 && index < this.images.length) {
                this.active = index;
                this.activeImage = this.images[this.active];
            }
        }
    }"
        x-init="
        window.addEventListener('open-fasilitas-modal', (event) => {
            show(event.detail);
        });

        window.addEventListener('keydown', (event) => {
            if (!open) return;

            if (event.key === 'Escape') {
                close();
            }

            if (event.key === 'ArrowLeft') {
                previous();
            }

            if (event.key === 'ArrowRight') {
                next();
            }
        });
    "
        x-show="open"
        x-cloak
        x-transition:enter="transition duration-300 ease-out"
        x-transition:enter-start="opacity-0"
        x-transition:enter-end="opacity-100"
        class="fixed inset-0 z-[9999]"
    >
        <div class="absolute inset-0 bg-black/80" x-on:click="close()"></div>
        <button
            type="button"
            x-on:click="close()"
            class="absolute right-8 top-7 z-[10000] flex h-12 w-12 items-center justify-center rounded-full bg-white text-2xl font-light text-[#1F2937] shadow-lg transition duration-200 hover:scale-105 hover:bg-gray-100"
            aria-label="Tutup"
        >
            <svg
                xmlns="http://www.w3.org/2000/svg"
                width="1em"
                height="1em"
                viewBox="0 0 24 24"
            >
                <path d="M0 0h24v24H0z" fill="none" />
                <path
                    fill="none"
                    stroke="currentColor"
                    stroke-linecap="round"
                    d="m6 6l12 12m0-12L6 18"
                />
            </svg>
        </button>
        <div
            class="relative flex h-full w-full items-center justify-center px-6"
            x-on:click.stop
        >
            <div
                class="relative flex w-full max-w-275 flex-col items-center"
            >
                <div class="flex w-full items-center gap-4 sm:gap-6">
                    <button
                        type="button"
                        x-on:click="previous()"
                        x-bind:disabled="active === 0"
                        class="flex h-9 w-9 shrink-0 items-center justify-center rounded-md bg-[#FFD000] transition hover:bg-[#e9bd00] disabled:cursor-not-allowed disabled:opacity-40"
                        aria-label="Gambar sebelumnya"
                    >
                        <svg
                            width="11"
                            height="21"
                            viewBox="0 0 11 21"
                            fill="none"
                            xmlns="http://www.w3.org/2000/svg"
                        >
                            <path
                                d="M9.37589 0.275208L0.267602 9.66008C0.182916 9.74724 0.115734 9.85075 0.0698967 9.96468C0.0240602 10.0786 0.000469208 10.2007 0.000469208 10.3241C0.000469208 10.4474 0.0240602 10.5695 0.0698967 10.6834C0.115734 10.7974 0.182916 10.9009 0.267602 10.988L9.37589 20.3729C9.5468 20.549 9.7786 20.6479 10.0203 20.6479C10.262 20.6479 10.4938 20.549 10.6647 20.3729C10.8356 20.1968 10.9316 19.958 10.9316 19.7089C10.9316 19.4599 10.8356 19.2211 10.6647 19.045L2.1997 10.3241L10.6647 1.60317C10.7493 1.51597 10.8165 1.41246 10.8623 1.29853C10.9081 1.1846 10.9316 1.0625 10.9316 0.939188C10.9316 0.815874 10.9081 0.693769 10.8623 0.579844C10.8165 0.465918 10.7493 0.362402 10.6647 0.275208C10.5801 0.188011 10.4796 0.118845 10.3691 0.0716553C10.2585 0.0244656 10.14 0.000177383 10.0203 0.000177383C9.90063 0.000177383 9.78212 0.0244656 9.67155 0.0716553C9.56098 0.118845 9.46052 0.188011 9.37589 0.275208Z"
                                fill="white"
                            />
                        </svg>
                    </button>
                    <div
                        class="relative h-100 w-full flex-1 overflow-hidden rounded-xl bg-white shadow-2xl"
                    >
                        <img
                            x-show="activeImage"
                            x-bind:src="activeImage ? activeImage.gambar : ''"
                            x-bind:alt="activeImage ? activeImage.nama : ''"
                            class="h-full w-full object-cover"
                        />
                    </div>
                    <button
                        type="button"
                        x-on:click="next()"
                        x-bind:disabled="active === images.length - 1"
                        class="flex h-9 w-9 shrink-0 items-center justify-center rounded-md bg-[#FFD000] transition hover:bg-[#e9bd00] disabled:cursor-not-allowed disabled:opacity-40"
                        aria-label="Gambar berikutnya"
                    >
                        <svg
                            width="11"
                            height="21"
                            viewBox="0 0 11 21"
                            fill="none"
                            xmlns="http://www.w3.org/2000/svg"
                        >
                            <path
                                d="M1.55575 20.3727L10.664 10.9879C10.7487 10.9007 10.8159 10.7972 10.8617 10.6833C10.9076 10.5693 10.9312 10.4472 10.9312 10.3239C10.9312 10.2006 10.9076 10.0784 10.8617 9.9645C10.8159 9.85057 10.7487 9.74707 10.664 9.65991L1.55575 0.275029C1.38484 0.098931 1.15304 0 0.911336 0C0.669634 0 0.437832 0.098931 0.266924 0.275029C0.0960149 0.451128 0 0.689969 0 0.939009C0 1.18805 0.0960149 1.42689 0.266924 1.60299L8.73194 10.3239L0.266924 19.0448C0.182298 19.132 0.11517 19.2355 0.0693709 19.3494C0.023572 19.4633 0 19.5855 0 19.7088C0 19.8321 0.023572 19.9542 0.0693709 20.0681C0.11517 20.182 0.182298 20.2855 0.266924 20.3727C0.351549 20.4599 0.452014 20.5291 0.562582 20.5763C0.673151 20.6235 0.791657 20.6478 0.911336 20.6478C1.03101 20.6478 1.14952 20.6235 1.26009 20.5763C1.37066 20.5291 1.47112 20.4599 1.55575 20.3727Z"
                                fill="white"
                            />
                        </svg>
                    </button>
                </div>
                <div class="mt-4 flex items-center justify-center gap-1.5">
                    <template
                        x-for="(image, index) in images"
                        x-bind:key="index"
                    >
                        <button
                            type="button"
                            x-on:click="goTo(index)"
                            x-bind:class="
                            active === index
                                ? 'w-16 bg-[#FFD000]'
                                : 'w-1.5 bg-white/70'
                        "
                            class="h-1.5 rounded-full transition-all duration-300"
                            x-bind:aria-label="'Gambar ' + (index + 1)"
                        ></button>
                    </template>
                </div>
            </div>
        </div>
    </div>
</template>
