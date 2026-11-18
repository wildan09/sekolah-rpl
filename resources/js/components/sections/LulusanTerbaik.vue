<script lang="ts">
export interface Graduate {
    id: number | string;
    label: string;
    name: string;
    major: string;
    graduationYear: number;
    job: string;
    motivation: string;
    image?: string | null;
    photo?: string | null;
}
</script>

<script setup lang="ts">
import {
    Briefcase,
    CalendarCheck,
    Quote,
    Star,
    Users,
    X,
} from "lucide-vue-next";
import {
    computed,
    onBeforeUnmount,
    onMounted,
    ref,
    watch,
    type Component,
} from "vue";

const props = withDefaults(
    defineProps<{
        title?: string;
        subtitle?: string;
        items: Graduate[];
    }>(),
    {
        title: "Lulusan Terbaik",
        subtitle:
            "Lulusan terbaik SMK Negeri 1 Purwosari yang telah menginspirasi melalui prestasi akademik karakter, dan dedikasi.",
    },
);

/* ───────────── Carousel ───────────── */
const track = ref<HTMLElement | null>(null);
const canPrev = ref(false);
const canNext = ref(false);
let resizeObserver: ResizeObserver | undefined;

function updateState() {
    const el = track.value;
    if (!el) return;
    const maxScroll = el.scrollWidth - el.clientWidth;
    canPrev.value = el.scrollLeft > 1;
    canNext.value = el.scrollLeft < maxScroll - 1;
}

function scrollByCard(direction: 1 | -1) {
    const el = track.value;
    const card = el?.firstElementChild as HTMLElement | null;
    if (!el || !card) return;

    const gap = parseFloat(getComputedStyle(el).columnGap) || 0;
    const reduceMotion = window.matchMedia(
        "(prefers-reduced-motion: reduce)",
    ).matches;

    el.scrollBy({
        left: direction * (card.offsetWidth + gap),
        behavior: reduceMotion ? "auto" : "smooth",
    });
}

onMounted(() => {
    updateState();
    if (track.value) {
        resizeObserver = new ResizeObserver(updateState);
        resizeObserver.observe(track.value);
    }
});

/* ───────────── Modal ───────────── */
const dialogRef = ref<HTMLDialogElement | null>(null);
const activeIndex = ref<number | null>(null);

const current = computed<Graduate | null>(() =>
    activeIndex.value === null
        ? null
        : (props.items[activeIndex.value] ?? null),
);

const rows = computed<{ label: string; value: string; icon: Component }[]>(
    () => {
        const g = current.value;
        if (!g) return [];
        return [
            { label: "Jurusan", value: g.major, icon: Users },
            {
                label: "Tahun Kelulusan",
                value: String(g.graduationYear),
                icon: CalendarCheck,
            },
            { label: "Pekerjaan", value: g.job, icon: Briefcase },
            { label: "Motivasi", value: `“${g.motivation}”`, icon: Quote },
        ];
    },
);

function lockScroll(locked: boolean) {
    document.documentElement.classList.toggle("overflow-hidden", locked);
}

watch(activeIndex, (value) => {
    const dialog = dialogRef.value;
    if (!dialog) return;

    if (value !== null && !dialog.open) {
        dialog.showModal();
        lockScroll(true);
    } else if (value === null && dialog.open) {
        dialog.close();
    }
});

function onDialogClose() {
    lockScroll(false);
    activeIndex.value = null;
}

function closeModal() {
    dialogRef.value?.close();
}

function goModal(step: 1 | -1) {
    if (activeIndex.value === null || props.items.length === 0) return;
    const total = props.items.length;
    activeIndex.value = (activeIndex.value + step + total) % total;
}

function onDialogClick(event: MouseEvent) {
    if (event.target === dialogRef.value) closeModal();
}

onBeforeUnmount(() => {
    resizeObserver?.disconnect();
    lockScroll(false);
});
</script>

<template>
    <section
        class="bg-white px-5 py-16 sm:px-8 sm:py-20 lg:px-[110px] lg:py-[130px]"
        aria-labelledby="graduates-title"
    >
        <div class="mx-auto max-w-[1200px]">
            <header class="mx-auto max-w-[694px] text-center">
                <h2
                    id="graduates-title"
                    class="text-3xl leading-tight font-bold text-secondary-60 lg:text-[48px]"
                >
                    {{ title }}
                </h2>
                <p
                    class="mt-[10px] text-base leading-snug text-neutral-40 lg:text-[22px] lg:leading-7"
                >
                    {{ subtitle }}
                </p>
            </header>

            <div
                class="mt-8 flex flex-wrap items-center justify-center gap-4 sm:mt-10 md:flex-nowrap md:gap-8 lg:gap-[55px]"
            >
                <button
                    type="button"
                    class="order-2 inline-flex size-10 shrink-0 items-center justify-center rounded-md bg-primary-60 text-white transition-colors duration-300 hover:bg-primary-50 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-primary-60 disabled:cursor-not-allowed disabled:opacity-40 md:order-1 lg:size-[45px]"
                    aria-label="Previous graduates"
                    :disabled="!canPrev"
                    @click="scrollByCard(-1)"
                >
                    <svg
                        class="size-5 lg:size-6"
                        viewBox="0 0 24 24"
                        fill="none"
                        stroke="currentColor"
                        stroke-width="1.5"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        aria-hidden="true"
                    >
                        <path d="m15 18-6-6 6-6" />
                    </svg>
                </button>

                <ul
                    ref="track"
                    class="order-1 -my-2 flex w-full snap-x snap-mandatory gap-6 overflow-x-auto scroll-smooth py-2 [scrollbar-width:none] md:order-2 md:w-auto md:min-w-0 md:flex-1 [&::-webkit-scrollbar]:hidden"
                    @scroll.passive="updateState"
                >
                    <li
                        v-for="(item, index) in items"
                        :key="item.id"
                        class="basis-full shrink-0 snap-start sm:basis-[calc((100%-1.5rem)/2)] lg:basis-[calc((100%-3rem)/3)]"
                    >
                        <article
                            class="relative isolate aspect-[322/290] w-full overflow-hidden rounded-lg bg-neutral-20/40 transition-transform duration-300 [clip-path:inset(0_round_8px)] hover:-translate-y-1 motion-reduce:transition-none motion-reduce:hover:translate-y-0"
                        >
                            <img
                                v-if="item.image"
                                :src="item.image"
                                alt=""
                                width="322"
                                height="290"
                                loading="lazy"
                                decoding="async"
                                class="size-full object-cover"
                            />
                            <h3
                                v-else
                                class="flex size-full items-center justify-center text-4xl font-bold text-secondary-60 lg:text-[40px]"
                            >
                                {{ item.label }}
                            </h3>

                            <button
                                type="button"
                                class="absolute inset-0 cursor-pointer focus-visible:outline-2 focus-visible:-outline-offset-2 focus-visible:outline-primary-60"
                                :aria-label="`Lihat profil lulusan ${item.name}`"
                                aria-haspopup="dialog"
                                @click="activeIndex = index"
                            />
                        </article>
                    </li>
                </ul>

                <button
                    type="button"
                    class="order-3 inline-flex size-10 shrink-0 items-center justify-center rounded-md bg-primary-60 text-white transition-colors duration-300 hover:bg-primary-50 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-primary-60 disabled:cursor-not-allowed disabled:opacity-40 lg:size-[45px]"
                    aria-label="Next graduates"
                    :disabled="!canNext"
                    @click="scrollByCard(1)"
                >
                    <svg
                        class="size-5 lg:size-6"
                        viewBox="0 0 24 24"
                        fill="none"
                        stroke="currentColor"
                        stroke-width="1.5"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        aria-hidden="true"
                    >
                        <path d="m9 18 6-6-6-6" />
                    </svg>
                </button>
            </div>
        </div>

        <dialog
            ref="dialogRef"
            class="m-auto max-h-[calc(100dvh-2rem)] w-[calc(100%-2rem)] max-w-[1060px] overflow-y-auto overscroll-contain bg-transparent p-0 transition-[opacity,scale] duration-200 backdrop:bg-black/80 [scrollbar-width:none] sm:max-h-none sm:overflow-visible starting:open:scale-95 starting:open:opacity-0 motion-reduce:transition-none [&::-webkit-scrollbar]:hidden"
            aria-labelledby="graduate-modal-title"
            @close="onDialogClose"
            @click="onDialogClick"
            @keydown.left.prevent="goModal(-1)"
            @keydown.right.prevent="goModal(1)"
        >
            <div v-if="current" class="flex flex-col items-center gap-4">
                <!-- Tinggi ditentukan isi: foto (rasio 340:422) + padding = ±470px, bukan tinggi fixed -->
                <article
                    class="relative flex w-full flex-col gap-5 rounded-2xl bg-white p-6 sm:flex-row sm:gap-6 lg:gap-9"
                >
                    <img
                        v-if="current.photo"
                        :src="current.photo"
                        :alt="`Foto ${current.name}`"
                        class="aspect-[16/10] w-full shrink-0 rounded-xl object-cover sm:aspect-[340/422] sm:w-[240px] sm:self-stretch lg:w-[340px]"
                    />
                    <div
                        v-else
                        class="aspect-[16/10] w-full shrink-0 rounded-xl bg-neutral-20/40 sm:aspect-[340/422] sm:w-[240px] sm:self-stretch lg:w-[340px]"
                        aria-hidden="true"
                    />

                    <div class="flex min-w-0 flex-1 flex-col sm:pr-4">
                        <span
                            class="inline-flex h-6 w-fit items-center gap-1.5 rounded-full bg-primary-10 px-3 text-xs font-medium text-secondary-60"
                        >
                            <Star
                                class="size-3 fill-primary-60 text-primary-60"
                                aria-hidden="true"
                            />
                            Lulusan Terbaik
                        </span>

                        <h2
                            id="graduate-modal-title"
                            class="mt-5 text-2xl leading-tight font-bold text-secondary-60 lg:mt-6 lg:text-[32px] lg:leading-10"
                        >
                            {{ current.name }}
                        </h2>

                        <dl class="mt-2 divide-y divide-neutral-20/60">
                            <div
                                v-for="row in rows"
                                :key="row.label"
                                class="grid gap-1 py-4 sm:grid-cols-[140px_1fr] sm:items-start sm:gap-0 lg:grid-cols-[222px_1fr]"
                            >
                                <dt
                                    class="flex items-center gap-3 leading-6 font-medium text-secondary-60"
                                >
                                    <component
                                        :is="row.icon"
                                        class="size-5 shrink-0 text-blue-500"
                                        aria-hidden="true"
                                    />
                                    {{ row.label }}
                                </dt>
                                <dd class="leading-6 text-neutral-40">
                                    {{ row.value }}
                                </dd>
                            </div>
                        </dl>
                    </div>

                    <button
                        type="button"
                        autofocus
                        class="absolute top-3 right-3 rounded-full bg-white/90 p-1 text-secondary-60 transition-colors hover:bg-neutral-20/40 focus-visible:outline-2 focus-visible:outline-primary-60 sm:top-[18px] sm:right-5 sm:bg-transparent"
                        aria-label="Tutup"
                        @click="closeModal"
                    >
                        <X class="size-6" aria-hidden="true" />
                    </button>
                </article>

                <div
                    v-if="items.length > 1"
                    class="flex items-center gap-1.5"
                    role="group"
                    aria-label="Pilih lulusan"
                >
                    <button
                        v-for="(item, index) in items"
                        :key="item.id"
                        type="button"
                        class="relative h-1.5 rounded-full transition-all duration-300 before:absolute before:-inset-2 motion-reduce:transition-none"
                        :class="
                            index === activeIndex
                                ? 'w-36 bg-primary-60'
                                : 'w-1.5 bg-neutral-40 hover:bg-neutral-30'
                        "
                        :aria-label="`Lihat ${item.name}`"
                        :aria-current="
                            index === activeIndex ? 'true' : undefined
                        "
                        @click="activeIndex = index"
                    />
                </div>
            </div>
        </dialog>
    </section>
</template>
