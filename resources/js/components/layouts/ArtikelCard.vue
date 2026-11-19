<script setup>
import { Link } from "@inertiajs/vue3";

defineProps({
    article: {
        type: Object,
        required: true,
    },
});
</script>

<template>
    <article
        class="flex items-center gap-[21px] rounded-2xl bg-white p-4 shadow-[0_2px_16px_rgba(0,0,0,0.06)] sm:p-3 lg:gap-5"
    >
        <div
            class="aspect-[220/228] w-28 shrink-0 overflow-hidden rounded-2xl sm:w-40 lg:w-[220px]"
        >
            <img
                v-if="article.thumbnail"
                :src="article.thumbnail"
                :alt="article.title"
                loading="lazy"
                class="size-full object-cover"
            />
            <div
                v-else
                class="thumb-placeholder size-full"
                aria-hidden="true"
            />
        </div>

        <div class="min-w-0 flex-1">
            <time
                :datetime="article.datetime"
                class="block text-xs text-primary-60 sm:text-xs"
            >
                {{ article.date }}
            </time>

            <h3
                class="mt-3 line-clamp-3 text-xl font-bold text-secondary-60 sm:mt-5 lg:text-[26px]"
            >
                {{ article.title }}
            </h3>

            <Link
                :href="article.href"
                class="group mt-5 inline-flex w-fit items-center gap-3.5 text-[20px] text-primary-60 transition-colors duration-300 hover:text-primary-40 focus-visible:outline-2 focus-visible:outline-offset-4 focus-visible:outline-primary-60"
            >
                Lihat detail
                <svg
                    class="shrink-0 transition-transform duration-300 ease-out group-hover:translate-x-1.5 group-focus-visible:translate-x-1.5 motion-reduce:transition-none motion-reduce:transform-none"
                    width="18"
                    height="15"
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
.thumb-placeholder {
    background: conic-gradient(
        #f1f1f1 25%,
        #fafafa 0 50%,
        #f1f1f1 0 75%,
        #fafafa 0
    );
    background-size: 16px 16px;
}
</style>
