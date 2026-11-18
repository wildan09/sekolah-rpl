<script lang="ts">
export interface News {
    id: number | string;
    title: string;
    excerpt: string;
    image: string;
    publishedAt: string;
    href: string;
    isImportant: boolean;
}

const dummyImage = "/images/berita-jetz.webp";

const newsMock: News[] = [
    {
        id: 1,
        title: "🎉Keseruan JETZ School Activation di SMKN 1 Purwosari!🎉",
        excerpt:
            'Hari ini, SMKN 1 Purwosari dipenuhi energi positif dan semangat luar biasa dalam acara "JETZ School Activation"! Acara ini merupakan wujud nyata sinergi antara dunia pendidikan dan dunia industri, menjalin kerja sama link and match yang luar biasa dengan PT Indofood Fortuna Makmur (Brand Jet-Z), PT Jaya Impian Abadi, dan agency Momentum Kreasindo.',
        image: "/images/berita-jetz.webp",
        publishedAt: "2026-09-06T08:00:00+07:00",
        href: "/berita/keseruan-jetz-school-activation",
        isImportant: true,
    },
    {
        id: 2,
        title: "Pengumuman PPDB Tahun Ajaran 2026/2027",
        excerpt: "Pendaftaran peserta didik baru dibuka mulai 1 Oktober 2026.",
        image: "/images/berita-ppdb.webp",
        publishedAt: "2026-09-04T10:00:00+07:00",
        href: "/berita/pengumuman-ppdb",
        isImportant: true,
    },
    {
        id: 3,
        title: "Siswa RPL Raih Juara 1 LKS Tingkat Provinsi dengan Karya Aplikasi Inovatif yang Dikembangkan Selama Enam Bulan",
        excerpt:
            "Tim RPL SMKN 1 Purwosari berhasil membawa pulang medali emas setelah menyisihkan puluhan sekolah dari seluruh provinsi.",
        image: "/images/berita-rpl.webp",
        publishedAt: "2026-08-28T09:30:00+07:00",
        href: "/berita/juara-lks",
        isImportant: false,
    },
    {
        id: 4,
        title: "Kunjungan Industri Jurusan TKJ ke Pusat Data",
        excerpt:
            "Siswa kelas XI TKJ mengunjungi pusat data untuk melihat langsung infrastruktur jaringan skala besar.",
        image: "/images/berita-tkj.webp",
        publishedAt: "2026-08-20T09:00:00+07:00",
        href: "/berita/kunjungan-industri-tkj",
        isImportant: false,
    },
    {
        id: 5,
        title: "Pameran Karya Siswa DKV 2026",
        excerpt:
            "Puluhan karya poster, ilustrasi, dan film pendek dipamerkan di aula sekolah.",
        image: "/images/berita-dkv.webp",
        publishedAt: "2026-08-12T13:00:00+07:00",
        href: "/berita/pameran-dkv",
        isImportant: false,
    },
    {
        id: 6,
        title: "Upacara Peringatan Hari Kemerdekaan ke-81",
        excerpt:
            "Seluruh warga sekolah mengikuti upacara bendera dengan khidmat.",
        image: "/images/berita-17-agustus.webp",
        publishedAt: "2026-08-17T07:00:00+07:00",
        href: "/berita/upacara-17-agustus",
        isImportant: false,
    },
];
</script>

<script setup lang="ts">
import { Link } from "@inertiajs/vue3";
import { ArrowRight, Star } from "lucide-vue-next";
import { computed, onMounted, ref } from "vue";

const props = withDefaults(
    defineProps<{
        items?: News[];
        eyebrow?: string;
        title?: string;
        ctaLabel?: string;
        ctaHref?: string;
    }>(),
    {
        eyebrow: "Berita Terbaru",
        title: "Informasi dan Kabar Terkini",
        ctaLabel: "Lihat Semua Berita",
        ctaHref: "/berita",
    },
);

const list = computed<News[]>(
    () => props.items ?? (import.meta.env.DEV ? newsMock : []),
);

const formatDate = (iso: string) =>
    new Intl.DateTimeFormat("id-ID", {
        day: "2-digit",
        month: "long",
        year: "numeric",
        timeZone: "Asia/Jakarta",
    }).format(new Date(iso));

const track = ref<HTMLElement | null>(null);
const activeIndex = ref(0);

function updateActive() {
    const el = track.value;
    if (!el || el.clientWidth === 0) return;
    activeIndex.value = Math.round(el.scrollLeft / el.clientWidth);
}

function goTo(index: number) {
    const el = track.value;
    if (!el) return;
    const reduceMotion = window.matchMedia(
        "(prefers-reduced-motion: reduce)",
    ).matches;
    el.scrollTo({
        left: index * el.clientWidth,
        behavior: reduceMotion ? "auto" : "smooth",
    });
}

onMounted(updateActive);
</script>

<template>
    <section
        v-if="list.length"
        class="bg-neutral-10 px-5 py-16 sm:px-8 sm:py-20 lg:px-[110px] lg:py-[100px]"
        aria-labelledby="news-title"
    >
        <div class="mx-auto max-w-[1220px]">
            <header
                class="flex flex-col gap-5 sm:flex-row sm:items-end sm:justify-between"
            >
                <div>
                    <p
                        class="text-base font-semibold text-primary-60 uppercase lg:text-xl"
                    >
                        {{ eyebrow }}
                    </p>
                    <h2
                        id="news-title"
                        class="heading-2 mt-1 text-secondary-60"
                    >
                        {{ title }}
                    </h2>
                </div>

                <Link
                    :href="ctaHref"
                    class="inline-flex w-fit shrink-0 items-center justify-center gap-5 rounded-lg bg-primary-60 px-5 py-3 text-sm font-medium text-secondary-60 transition-colors duration-300 hover:bg-primary-50 sm:text-base"
                >
                    {{ ctaLabel }}
                    <ArrowRight
                        class="size-5"
                        :stroke-width="1.5"
                        aria-hidden="true"
                    />
                </Link>
            </header>

            <div
                class="isolate mt-6 overflow-hidden rounded-[20px] sm:rounded-[28px] lg:mt-8 lg:rounded-[30px]"
            >
                <ul
                    ref="track"
                    class="flex snap-x snap-mandatory overflow-x-auto [scrollbar-width:none] focus-visible:outline-2 focus-visible:-outline-offset-2 focus-visible:outline-primary-60 [&::-webkit-scrollbar]:hidden"
                    tabindex="0"
                    aria-label="Berita terbaru"
                    @scroll.passive="updateActive"
                >
                    <li
                        v-for="(item, index) in list"
                        :key="item.id"
                        class="flex basis-full shrink-0 snap-center"
                        aria-roledescription="slide"
                        :aria-label="`${index + 1} dari ${list.length}`"
                    >
                        <article
                            class="relative flex min-h-[460px] w-full flex-col justify-end overflow-hidden bg-secondary-60 sm:min-h-[500px] lg:aspect-[1220/579] lg:min-h-0"
                        >
                            <img
                                :src="item.image"
                                alt=""
                                width="1220"
                                height="579"
                                :loading="index === 0 ? 'eager' : 'lazy'"
                                decoding="async"
                                class="absolute inset-0 size-full object-cover"
                            />

                            <div
                                class="absolute inset-0 bg-linear-to-b/srgb from-[#666666]/30 from-0% to-black to-100%"
                                aria-hidden="true"
                            />

                            <span
                                v-if="item.isImportant"
                                class="absolute top-4 right-4 inline-flex h-[34px] items-center gap-[7px] rounded-full bg-secondary-60 px-3.5 text-sm font-medium text-primary-60 shadow-[0_0_30px_0_rgb(255_193_7/0.6)] lg:top-[30px] lg:right-[30px]"
                            >
                                <Star
                                    class="size-4 fill-primary-60"
                                    aria-hidden="true"
                                />
                                Berita Penting
                            </span>

                            <div
                                class="relative flex flex-col px-5 pt-20 pb-8 sm:px-8 lg:p-[30px]"
                            >
                                <time
                                    :datetime="item.publishedAt"
                                    class="text-sm text-primary-60"
                                >
                                    {{ formatDate(item.publishedAt) }}
                                </time>

                                <h3
                                    class="heading-5 mt-3 line-clamp-2 text-neutral-10"
                                >
                                    {{ item.title }}
                                </h3>

                                <p
                                    class="mt-2 line-clamp-3 text-sm leading-relaxed text-neutral-30 sm:text-base lg:text-lg lg:text-justify"
                                >
                                    {{ item.excerpt }}
                                </p>

                                <Link
                                    :href="item.href"
                                    class="mt-4 inline-flex w-fit items-center gap-2 text-sm font-medium text-primary-60 transition-colors duration-300 hover:text-primary-40 focus-visible:outline-2 focus-visible:outline-offset-4 focus-visible:outline-primary-60"
                                >
                                    Lihat detail
                                    <ArrowRight
                                        class="size-4"
                                        :stroke-width="1.5"
                                        aria-hidden="true"
                                    />
                                </Link>
                            </div>
                        </article>
                    </li>
                </ul>
            </div>

            <div
                v-if="list.length > 1"
                class="mt-3.5 flex items-center justify-center gap-1.5"
                role="group"
                aria-label="Pilih berita"
            >
                <button
                    v-for="(item, index) in list"
                    :key="item.id"
                    type="button"
                    class="relative h-1.5 rounded-full transition-all duration-300 before:absolute before:-inset-x-0.5 before:-inset-y-3 motion-reduce:transition-none"
                    :class="
                        index === activeIndex
                            ? 'w-36 bg-primary-60'
                            : 'w-1.5 bg-neutral-50 hover:bg-neutral-40'
                    "
                    :aria-label="`Lihat berita ${index + 1}: ${item.title}`"
                    :aria-current="index === activeIndex ? 'true' : undefined"
                    @click="goTo(index)"
                />
            </div>
        </div>
    </section>
</template>
