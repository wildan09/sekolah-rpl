<script setup>
import { ref, computed } from "vue";
import { Link } from "@inertiajs/vue3";
const NOMOR_WA = "6281234567890"; // format 62xxxxxxxxxx

const produk = {
    nama: "Bibit Tanaman Cabai",
    harga: 25000,
    deskripsi:
        "Bibit tanaman cabai yang cocok untuk kebutuhan budidaya dan dapat digunakan untuk skala rumah tangga maupun usaha. Bibit siap tanam dan telah melalui proses seleksi untuk memastikan kualitas tanaman yang baik. Cocok ditanam di berbagai media dan menjadi pilihan bagi Anda yang ingin memulai atau mengembangkan budidaya cabai dengan praktis dan mudah.",
    stok: 150,
    satuan: "Pack",
    kategori: "Pertanian",
    asal: "SMK Negeri 1 Purwosari",
    ringkas: "Bibit cabai siap tanam",
    kualitas: "Bibit unggul, dan sehat",
    pengiriman: "Pengiriman cepat, aman, dan terpercaya selamat sampai tujuan",
    galeri: [
        "/images/produk/bibit-cabai.jpg",
        "/images/produk/bibit-cabai-2.jpg",
        "/images/produk/bibit-cabai-3.jpg",
    ],
};
const activeFoto = ref(0);
const tersedia = produk.stok > 0;
const rupiah = (n) => "Rp" + Number(n).toLocaleString("id-ID");

const linkWhatsApp = `https://wa.me/${NOMOR_WA}?text=${encodeURIComponent(
    `Halo admin, saya ingin memesan produk "${produk.nama}" (${rupiah(produk.harga)}). Apakah stoknya masih tersedia?`,
)}`;
const ikon = {
    kategori:
        '<rect width="7" height="7" x="3" y="3" rx="1"/><rect width="7" height="7" x="14" y="3" rx="1"/><rect width="7" height="7" x="14" y="14" rx="1"/><rect width="7" height="7" x="3" y="14" rx="1"/>',
    satuan: '<path d="m7.5 4.27 9 5.15"/><path d="M21 8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16Z"/><path d="m3.3 7 8.7 5 8.7-5"/><path d="M12 22V12"/>',
    harga: '<path d="M12.586 2.586A2 2 0 0 0 11.172 2H4a2 2 0 0 0-2 2v7.172a2 2 0 0 0 .586 1.414l8.704 8.704a2.426 2.426 0 0 0 3.42 0l6.58-6.58a2.426 2.426 0 0 0 0-3.42z"/><circle cx="7.5" cy="7.5" r=".5" fill="currentColor"/>',
    ok: '<circle cx="12" cy="12" r="10"/><path d="m9 12 2 2 4-4"/>',
    asal: '<path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/><circle cx="12" cy="10" r="3"/>',
    deskripsi:
        '<path d="M15 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7Z"/><path d="M14 2v4a2 2 0 0 0 2 2h4"/><path d="M10 9H8"/><path d="M16 13H8"/><path d="M16 17H8"/>',
    kualitas:
        '<path d="M20 13c0 5-3.5 7.5-7.66 8.95a1 1 0 0 1-.67-.01C7.5 20.5 4 18 4 13V6a1 1 0 0 1 1-1c2 0 4.5-1.2 6.24-2.72a1.17 1.17 0 0 1 1.52 0C14.51 3.81 17 5 19 5a1 1 0 0 1 1 1z"/><path d="m9 12 2 2 4-4"/>',
    pengiriman:
        '<path d="M14 18V6a2 2 0 0 0-2-2H4a2 2 0 0 0-2 2v11a1 1 0 0 0 1 1h2"/><path d="M15 18H9"/><path d="M19 18h2a1 1 0 0 0 1-1v-3.65a1 1 0 0 0-.22-.624l-3.48-4.35A1 1 0 0 0 17.52 8H14"/><circle cx="17" cy="18" r="2"/><circle cx="7" cy="18" r="2"/>',
    whatsapp: '<path d="M7.9 20A9 9 0 1 0 4 16.1L2 22Z"/>',
};

const infoKiri = [
    { label: "Kategori", nilai: produk.kategori, ikon: ikon.kategori },
    { label: "Satuan", nilai: produk.satuan, ikon: ikon.satuan },
    {
        label: "Harga",
        nilai: Number(produk.harga).toLocaleString("id-ID"),
        ikon: ikon.harga,
    },
    {
        label: "Ketersediaan",
        nilai: tersedia ? "Tersedia" : "Habis",
        ikon: ikon.ok,
    },
];

const infoKanan = [
    { label: "Asal Produk", nilai: produk.asal, ikon: ikon.asal },
    { label: "Deskripsi", nilai: produk.ringkas, ikon: ikon.deskripsi },
    { label: "Kualitas", nilai: produk.kualitas, ikon: ikon.kualitas },
    { label: "Pengiriman", nilai: produk.pengiriman, ikon: ikon.pengiriman },
];
</script>

<template>
    <main class="w-full px-4 py-6 sm:px-8 sm:py-8">
        <div class="mx-auto max-w-[900px]">
            <Link
                href="/"
                class="inline-flex items-center gap-2 text-[11px] font-medium text-[#1F2937] transition hover:opacity-70"
            >
                <span
                    class="flex h-5 w-5 items-center justify-center rounded-full bg-[#FFC107]"
                >
                    <svg
                        width="11"
                        height="11"
                        viewBox="0 0 24 24"
                        fill="none"
                        stroke="white"
                        stroke-width="3"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                    >
                        <path d="M19 12H5" />
                        <path d="m12 19-7-7 7-7" />
                    </svg>
                </span>
                Kembali
            </Link>
            <div class="mt-4 grid grid-cols-1 gap-6 md:grid-cols-2 md:gap-8">
                <!-- Galeri -->
                <div>
                    <div
                        class="aspect-square w-full overflow-hidden rounded-xl bg-gray-100"
                    >
                        <img
                            :src="produk.galeri[activeFoto]"
                            :alt="produk.nama"
                            class="h-full w-full object-cover"
                        />
                    </div>

                    <div class="mt-2.5 grid grid-cols-3 gap-2.5">
                        <button
                            v-for="(foto, i) in produk.galeri"
                            :key="i"
                            type="button"
                            @click="activeFoto = i"
                            :class="
                                activeFoto === i
                                    ? 'ring-2 ring-[#FFC107]'
                                    : 'opacity-80 hover:opacity-100'
                            "
                            class="aspect-[1.6/1] overflow-hidden rounded-lg bg-gray-100 transition"
                            :aria-label="'Foto ' + (i + 1)"
                        >
                            <img
                                :src="foto"
                                :alt="produk.nama + ' ' + (i + 1)"
                                class="h-full w-full object-cover"
                            />
                        </button>
                    </div>
                </div>
                <div class="flex min-w-0 flex-col">
                    <h1
                        class="text-[26px] font-bold leading-tight text-[#1F2937] sm:text-[30px]"
                    >
                        {{ produk.nama }}
                    </h1>

                    <p
                        class="mt-3 text-[22px] font-semibold text-[#FFC107] sm:text-[24px]"
                    >
                        {{ rupiah(produk.harga) }}
                    </p>

                    <p
                        class="mt-4 text-justify text-[14px] leading-[1.7] text-[#A3A3A3]"
                    >
                        {{ produk.deskripsi }}
                    </p>

                    <div
                        :class="tersedia ? 'bg-[#FFF3D6]' : 'bg-red-50'"
                        class="mt-5 flex items-start gap-3 rounded-xl px-4 py-3.5"
                    >
                        <svg
                            width="22"
                            height="22"
                            viewBox="0 0 24 24"
                            fill="none"
                            :stroke="tersedia ? '#E0A800' : '#DC2626'"
                            stroke-width="2"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            class="mt-0.5 shrink-0"
                            v-html="ikon.ok"
                        ></svg>
                        <div>
                            <p class="text-[15px] font-semibold text-[#1F2937]">
                                {{ tersedia ? "Tersedia" : "Stok Habis" }}
                            </p>
                            <p
                                v-if="tersedia"
                                class="text-[14px] text-[#A3A3A3]"
                            >
                                Stok: {{ produk.stok }}
                                {{ produk.satuan.toLowerCase() }}
                            </p>
                        </div>
                    </div>
                </div>
            </div>
            <div
                class="mt-8 rounded-xl bg-white p-4 shadow-[0_2px_16px_rgba(0,0,0,0.07)] sm:p-5"
            >
                <h2 class="inline-block text-[15px] font-bold text-[#1F2937]">
                    Informasi Produk
                </h2>
                <div class="mt-1 h-[2px] w-10 rounded bg-[#FFC107]"></div>

                <div class="mt-3 grid grid-cols-1 md:grid-cols-2">
                    <div class="md:pr-6">
                        <div
                            v-for="row in infoKiri"
                            :key="row.label"
                            class="grid grid-cols-[120px_1fr] items-start gap-2 border-b border-gray-200 py-3 last:border-b-0"
                        >
                            <span
                                class="flex items-center gap-2 text-[12px] font-medium text-[#1F2937]"
                            >
                                <svg
                                    width="14"
                                    height="14"
                                    viewBox="0 0 24 24"
                                    fill="none"
                                    stroke="#FFC107"
                                    stroke-width="2"
                                    stroke-linecap="round"
                                    stroke-linejoin="round"
                                    class="shrink-0"
                                    v-html="row.ikon"
                                ></svg>
                                {{ row.label }}
                            </span>
                            <span class="text-[12px] text-[#A3A3A3]">{{
                                row.nilai
                            }}</span>
                        </div>
                    </div>

                    <div class="md:border-l md:border-gray-200 md:pl-6">
                        <div
                            v-for="row in infoKanan"
                            :key="row.label"
                            class="grid grid-cols-[120px_1fr] items-start gap-2 border-b border-gray-200 py-3 last:border-b-0"
                        >
                            <span
                                class="flex items-center gap-2 text-[12px] font-medium text-[#1F2937]"
                            >
                                <svg
                                    width="14"
                                    height="14"
                                    viewBox="0 0 24 24"
                                    fill="none"
                                    stroke="#FFC107"
                                    stroke-width="2"
                                    stroke-linecap="round"
                                    stroke-linejoin="round"
                                    class="shrink-0"
                                    v-html="row.ikon"
                                ></svg>
                                {{ row.label }}
                            </span>
                            <span
                                class="text-[12px] leading-snug text-[#A3A3A3]"
                                >{{ row.nilai }}</span
                            >
                        </div>
                    </div>
                </div>
            </div>
            <div
                class="mt-5 rounded-xl border border-[#BFE6CB] bg-[#E8F8EE] p-4"
            >
                <div class="flex items-center gap-3">
                    <span
                        class="flex h-10 w-10 shrink-0 items-center justify-center rounded-full bg-[#25D366] text-white sm:h-11 sm:w-11"
                    >
                        <svg
                            width="22"
                            height="22"
                            viewBox="0 0 24 24"
                            fill="none"
                            stroke="currentColor"
                            stroke-width="2"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            v-html="ikon.whatsapp"
                        ></svg>
                    </span>
                    <div class="min-w-0">
                        <p class="text-[15px] font-semibold text-[#1F2937]">
                            Ingin memesan produk ini?
                        </p>
                        <p
                            class="text-[12px] leading-snug text-[#A3A3A3] sm:text-[14px]"
                        >
                            Hubungi admin kami melalui WhatsApp untuk informasi
                            ketersediaan stok, harga grosir, dan proses
                            pemesanan dengan mudah.
                        </p>
                    </div>
                </div>
            </div>

            <a
                :href="linkWhatsApp"
                target="_blank"
                rel="noopener"
                class="mt-2 flex h-9 w-full items-center justify-center rounded-md bg-[#25D366] text-[12px] font-medium text-white transition hover:bg-[#1fb857]"
            >
                Hubungi Admin via WhatsApp
            </a>
        </div>
    </main>
</template>
