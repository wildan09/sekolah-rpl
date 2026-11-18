<script setup lang="ts">
import { Link } from "@inertiajs/vue3";

withDefaults(
    defineProps<{
        headline?: string;
        tagline?: string;
        description?: string;
        ctaLabel?: string;
        ctaHref?: string;
        imageSrc?: string;
        imageAlt?: string;
    }>(),
    {
        headline: "Belajar, Berkarya, dan Berinovasi",
        tagline: "Bersama SMK Negeri 1 Purwosari",
        description:
            "Mewujudkan generasi yang Aktif, Kreatif, Inovatif, dan Berprestasi siap menghadapi dunia kerja.",
        ctaLabel: "Profil Sekolah",
        ctaHref: "/profil",
        imageSrc: "/images/hero-image.webp",
        imageAlt: "Gedung SMK Negeri 1 Purwosari",
    },
);
</script>

<template>
    <section
        class="relative isolate flex min-h-[620px] flex-col overflow-hidden rounded-b-[32px] bg-brand-navy shadow-hero sm:min-h-[680px] sm:rounded-b-[56px] lg:min-h-[780px] lg:rounded-b-[80px] xl:h-[940px]"
    >
        <img
            :src="imageSrc"
            :alt="imageAlt"
            width="1440"
            height="940"
            fetchpriority="high"
            decoding="async"
            class="absolute inset-0 -z-10 size-full object-cover object-center"
        />
>
        <div
            class="absolute inset-0 -z-10 bg-linear-to-b/srgb from-[#666666]/60 to-black"
            aria-hidden="true"
        />

        <div
            class="mx-auto flex w-full max-w-[1440px] flex-1 items-center px-5 pt-[118px] pb-16 sm:px-8 md:px-12 lg:px-[80px] xl:px-[110px]"
        >
            <div class="w-full max-w-[900px]">
                <h1
                    class="max-w-[848px] text-[clamp(2.25rem,5.5vw,4.125rem)] leading-[1.4] font-bold tracking-tight text-white uppercase"
                >
                    {{ headline }}
                </h1>

                <p
                    class="mt-4 text-[clamp(1.5rem,3.5vw,3rem)] leading-tight font-bold text-primary-60"
                >
                    {{ tagline }}
                </p>

                <p
                    class="mt-5 max-w-[640px] text-base leading-[1.3] text-neutral-40 sm:mt-6 sm:text-lg lg:text-xl"
                >
                    {{ description }}
                </p>

                <Link
                    :href="ctaHref"
                    class="mt-7 inline-flex items-center justify-center gap-4 rounded-xl bg-primary-60 px-5 py-3 text-sm font-semibold text-secondary-60 transition-colors duration-300 hover:bg-primary-50 sm:mt-8 sm:gap-5 sm:px-6 sm:py-3.5 sm:text-base"
                >
                    {{ ctaLabel }}

                    <svg
                        class="size-5 shrink-0 sm:size-6"
                        viewBox="0 0 24 24"
                        fill="none"
                        xmlns="http://www.w3.org/2000/svg"
                        aria-hidden="true"
                    >
                        <path
                            d="M20.7806 12.531L14.0306 19.281C13.8899 19.4218 13.699 19.5008 13.5 19.5008C13.301 19.5008 13.1101 19.4218 12.9694 19.281C12.8286 19.1403 12.7496 18.9494 12.7496 18.7504C12.7496 18.5514 12.8286 18.3605 12.9694 18.2198L18.4397 12.7504H3.75C3.55109 12.7504 3.36032 12.6714 3.21967 12.5307C3.07902 12.3901 3 12.1993 3 12.0004C3 11.8015 3.07902 11.6107 3.21967 11.4701L18.4397 11.2504L12.9694 5.78104C12.8286 5.64031 12.7496 5.44944 12.7496 5.25042C12.7496 5.05139 12.8286 4.86052 13.1101 4.71979L13.5 4.5C13.699 4.5 13.8899 4.57906 14.0306 4.71979L20.7806 11.4698C20.8504 11.5394 20.9057 11.6222 20.9434 11.7132C20.9812 11.8043 21.0006 11.9019 21.0006 12.0004C21.0006 12.099 20.9812 12.1966 20.9434 12.2876C20.9057 12.3787 20.8504 12.4614 20.7806 12.531Z"
                            fill="#132133"
                        />
                    </svg>
                </Link>
            </div>
        </div>
    </section>
</template>
