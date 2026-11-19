<script setup>
import { Link } from "@inertiajs/vue3";

defineProps({
    program: {
        type: Object,
        required: true,
        // { id, title, description, category, tone, image?, href }
    },
});

// Class harus berupa string utuh agar terdeteksi Tailwind (jangan dirakit dinamis).
const toneClasses = {
    primary: "bg-primary-60 text-secondary-60",
    blue: "bg-[#8197F7] text-secondary-60",
};
</script>

<template>
    <article
        class="flex h-full w-full max-w-[420px] flex-col overflow-hidden rounded-xl bg-white shadow-[0_2px_16px_rgba(0,0,0,0.06)]"
    >
        <!-- Gambar + badge kategori -->
        <div class="relative aspect-[19/10] w-full shrink-0">
            <img
                v-if="program.image"
                :src="program.image"
                :alt="program.title"
                loading="lazy"
                class="size-full object-cover"
            />
            <div
                v-else
                class="photo-placeholder size-full"
                aria-hidden="true"
            />

            <span
                class="absolute left-3 top-3 rounded-md px-2.5 py-1 text-[10px] font-medium leading-none sm:text-xs"
                :class="toneClasses[program.tone] ?? toneClasses.primary"
            >
                {{ program.category }}
            </span>
        </div>

        <!-- Konten -->
        <div class="flex flex-1 flex-col p-4 sm:p-5">
            <h3 class="heading-5 text-secondary-60">
                {{ program.title }}
            </h3>

            <p
                class="mt-2 line-clamp-3 text-sm leading-snug text-neutral-40 lg:text-base"
            >
                {{ program.description }}
            </p>

            <Link
                :href="program.href"
                class="group mt-4 inline-flex w-fit items-center gap-2.5 text-sm text-primary-60 transition-colors duration-300 hover:text-primary-70 focus-visible:outline-2 focus-visible:outline-offset-4 focus-visible:outline-primary-60 sm:text-base"
            >
                Lihat detail
                <svg
                    class="h-3 w-3.5 shrink-0 transition-transform duration-300 ease-out group-hover:translate-x-1.5 group-focus-visible:translate-x-1.5 motion-reduce:transition-none motion-reduce:transform-none sm:h-[15px] sm:w-[18px]"
                    viewBox="0 0 18 15"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                    aria-hidden="true"
                >
                    <path
                        d="M17.7806 8.03104L11.0306 14.781C10.8899 14.9218 10.699 15.0008 10.5 15.0008C10.301 15.0008 10.1101 14.9218 9.96937 14.781C9.82864 14.6403 9.74958 14.4494 9.74958 14.2504C9.74958 14.0514 9.82864 13.8605 9.96937 13.7198L15.4397 8.25042H0.75C0.551088 8.25042 0.360322 8.1714 0.21967 8.03075C0.0790178 7.8901 0 7.69933 0 7.50042C0 7.3015 0.0790178 7.11074 0.21967 6.97009C0.360322 6.82943 0.551088 6.75042 0.75 6.75042H15.4397L9.96937 1.28104C9.82864 1.14031 9.74958 0.94944 9.74958 0.750417C9.74958 0.551394 9.82864 0.360523 9.96937 0.219792C10.1101 0.0790615 10.301 0 10.5 0C10.699 0 10.8899 0.0790615 11.0306 0.219792L17.7806 6.96979C17.8504 7.03945 17.9057 7.12216 17.9434 7.21321C17.9812 7.30426 18.0006 7.40186 18.0006 7.50042C18.0006 7.59898 17.9812 7.69657 17.9434 7.78762C17.9057 7.87867 17.8504 7.96139 17.7806 8.03104Z"
                        fill="currentColor"
                    />
                </svg>
            </Link>
        </div>
    </article>
</template>

<style scoped>
.photo-placeholder {
    background: conic-gradient(
        #f1f1f1 25%,
        #fafafa 0 50%,
        #f1f1f1 0 75%,
        #fafafa 0
    );
    background-size: 16px 16px;
}
</style>