<script setup>
const misiList = [
    "Membekali peserta didik dengan keterampilan, pengetahuan.",
    "Menginstalasi software aplikasi spesifik.",
    "Menginstalasi software aplikasi spesifik.",
    "Membangun software aplikasi mulai dari website, desktop dan Android.",
    "Mengelola usaha di bidang pembuatan software aplikasi.",
];
</script>

<template>
    <div
        class="flex w-full flex-col gap-5 px-4 py-6 sm:px-8 lg:flex-row lg:px-27.5"
    >
        <div
            class="relative flex h-auto w-full flex-col justify-center gap-5 overflow-hidden rounded-[20px] bg-[#FFF8E8] px-6 py-5 lg:h-90 lg:w-88.75 lg:shrink-0 lg:gap-[20.04px] lg:px-10"
        >
            <div
                class="pointer-events-none absolute right-0 top-0 h-30.75 w-39.25"
                style="
                    background-image: radial-gradient(
                        #aaaaaa 1.5px,
                        transparent 1.5px
                    );
                    background-size: 8px 8px;
                    mask-image: radial-gradient(
                        circle at 100% 0%,
                        black 0%,
                        black 35%,
                        transparent 80%
                    );
                    -webkit-mask-image: radial-gradient(
                        circle at 100% 0%,
                        black 0%,
                        black 35%,
                        transparent 80%
                    );
                "
            ></div>

            <div
                class="pointer-events-none absolute bottom-0 left-0 h-30.75 w-39.25"
                style="
                    background-image: radial-gradient(
                        #aaaaaa 1.5px,
                        transparent 1.5px
                    );
                    background-size: 8px 8px;
                    mask-image: radial-gradient(
                        circle at 0% 100%,
                        black 0%,
                        black 35%,
                        transparent 80%
                    );
                    -webkit-mask-image: radial-gradient(
                        circle at 0% 100%,
                        black 0%,
                        black 35%,
                        transparent 80%
                    );
                "
            ></div>

            <div class="relative z-10 flex items-center gap-4">
                <div
                    class="flex h-10 w-10 shrink-0 items-center justify-center rounded-full bg-[#FFD45C]"
                >
                    <img src="/icons/eye.svg" alt="Visi" class="h-5 w-5" />
                </div>

                <h2 class="text-2xl font-semibold text-[#1F2937] lg:text-3xl">
                    Visi
                </h2>
            </div>

            <p
                class="relative z-10 text-base leading-5 text-[#A3A3A3] lg:text-xl"
            >
                “Mewujudkan SMK Yang Unggul, Berkarakter Dan Berdaya Saing
                Global Untuk Mendukung Jawa Timur Cerdas Yang Berkelanjutan”
            </p>
        </div>
        <div
            class="flex h-auto min-w-0 flex-1 flex-col gap-5 rounded-[20px] bg-[#FFF8E8] px-4 py-5 lg:h-90 lg:px-3.75"
        >
            <h2 class="text-2xl font-semibold text-[#1F2937] lg:text-3xl">
                Misi
            </h2>
            <div
                class="flex flex-col gap-2.5 sm:flex-row sm:flex-wrap lg:flex-nowrap"
            >
                <div
                    v-for="(misi, index) in misiList"
                    :key="index"
                    class="flex h-auto w-full min-w-0 flex-col items-center gap-5.5 rounded-[10px] bg-white px-3.5 py-5 text-center sm:w-[calc(50%-5px)] lg:h-[252.56px] lg:w-auto lg:flex-1"
                >
                    <div
                        class="flex h-11 w-11 shrink-0 items-center justify-center rounded-full bg-[#FFD45C] text-xl font-semibold text-black"
                    >
                        {{ index + 1 }}
                    </div>
                    <p class="text-sm leading-5 text-[#A3A3A3]">
                        {{ misi }}
                    </p>
                </div>
            </div>
        </div>
    </div>
</template>
