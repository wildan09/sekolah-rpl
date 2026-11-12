<script setup>
const steps = [
    {
        title: "Ketentuan SPMB",
        description:
            "Pahami terlebih dahulu syarat, ketentuan, dan prosedur SPMB Jawa Timur 2026",
        image: "/images/spmb/ketentuan-spmb.png",
    },
    {
        title: "Verifikasi Rapor",
        description:
            "Lakukan pengecekan verifikasi rapor semester 1 sampai semester 5 dari SMP/MTs/Sederajat yang bersangkutan",
        image: "/images/spmb/verifikasi-rapor.png",
    },
    {
        title: "Pengambilan PIN",
        description:
            "Lakukan pengambilan PIN yang akan digunakan untuk melakukan registrasi SPMB Jawa Timur 2026",
        image: "/images/spmb/pengambilan-pin.png",
    },
    {
        title: "Pendaftaran SPMB",
        description:
            "Pastikan seluruh data yang anda masukkan benar dan sesuai, setelah berhasil mendaftar, anda harus melakukan cetak bukti pendaftaran",
        image: "/images/spmb/pendaftaran-spmb.png",
    },
];
</script>

<template>
    <section class="mx-auto w-full px-4 py-10 sm:px-8 lg:px-27.5 lg:py-16">
        <div class="mx-auto mb-12 max-w-2xl text-center lg:mb-16">
            <span
                class="inline-block rounded-full bg-[#FFC107] px-4 py-1.5 text-xs font-semibold text-[#1F2937] sm:text-sm"
            >
                TAHAPAN PENDAFTARAN
            </span>
            <h2
                class="mt-4 text-2xl font-bold text-[#1F2937] sm:text-3xl lg:text-4xl"
            >
                SPMB Jawa Timur
            </h2>
            <p class="mt-2 text-sm text-[#A3A3A3] sm:text-base">
                Ikuti setiap tahapan dengan teliti agar proses pendaftaran
                berjalan lancar.
            </p>
        </div>
        <div class="flex w-full flex-col gap-7">
            <div v-for="(step, index) in steps" :key="index">
                <div
                    class="flex items-start gap-4 rounded-2xl bg-white p-4 shadow-sm xl:hidden"
                >
                    <div
                        class="flex h-100x w-9 shrink-0 items-center justify-center rounded-full bg-[#FFC107] text-base font-semibold leading-none text-black"
                    >
                        {{ index + 1 }}
                    </div>

                    <img
                        :src="step.image"
                        :alt="step.title"
                        class="h-16 w-16 shrink-0 object-contain sm:h-20 sm:w-20"
                    />

                    <div class="min-w-0 flex-1">
                        <h3
                            class="text-sm font-bold leading-5 text-[#1F2937] sm:text-base"
                        >
                            {{ step.title }}
                        </h3>

                        <p
                            class="mt-1 text-xs leading-5 text-[#A3A3A3] sm:text-sm"
                        >
                            {{ step.description }}
                        </p>
                    </div>
                </div>

                <div
                    class="relative hidden w-full items-center xl:flex"
                    :class="index % 2 === 0 ? 'flex-row' : 'flex-row-reverse'"
                >
                    <div
                        class="flex h-50 w-[50%] shrink-0 items-center gap-5 rounded-[20px] bg-white px-5 py-5 shadow-sm transition-all duration-300 hover:-translate-y-1 hover:shadow-lg"
                        :class="
                            index % 2 === 0
                                ? 'flex-row'
                                : 'flex-row-reverse text-left'
                        "
                    >
                        <img
                            :src="step.image"
                            :alt="step.title"
                            class="h-32.5 w-52.5 shrink-0 object-contain"
                        />

                        <div class="min-w-0 flex-1">
                            <h3
                                class="text-[22px] font-bold leading-6 text-[#1F2937]"
                            >
                                {{ step.title }}
                            </h3>

                            <p
                                class="mt-2 text-[20px] leading-5.25 text-[#A3A3A3]"
                            >
                                {{ step.description }}
                            </p>
                        </div>
                    </div>
                    <div
                        class="flex w-50 shrink-0 items-center"
                        :class="
                            index % 2 === 0 ? 'flex-row' : 'flex-row-reverse'
                        "
                    >
                        <div
                            class="w-62.5 shrink-0 border-t border-dashed border-[#AAAAAA]"
                        ></div>
                        <div
                            class="flex h-15 w-15 shrink-0 items-center justify-center rounded-full bg-[#FFC107] text-2xl font-semibold leading-none text-black"
                        >
                            {{ index + 1 }}
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div
            class="relative mt-10 flex flex-col items-center gap-6 overflow-hidden rounded-2xl bg-[#EAF0FE] p-6 sm:p-8 lg:mt-14 lg:flex-row lg:gap-10 lg:p-10"
        >
            <div
                class="pointer-events-none absolute right-0 top-0 h-37.5 w-57.5"
                style="
                    background-image: radial-gradient(
                        #6b7280 1.5px,
                        transparent 1.5px
                    );
                    background-size: 7px 7px;
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
            <img
                src="/images/spmb/spmb-jatim-illustration.png"
                alt="SPMB Jatim"
                class="relative z-10 h-32 w-auto shrink-0 sm:h-36"
            />

            <div class="relative z-10 flex-1 text-center lg:text-left">
                <h3 class="text-lg font-semibold text-[#1F2937] sm:text-xl">
                    Informasi Lengkap SPMB
                </h3>
                <p class="mt-2 text-sm leading-6 text-[#6B7280] sm:text-base">
                    Untuk informasi lengkap mengenai persyaratan, jadwal, jalur
                    pendaftaran, dan pengumuman penerimaan, silakan kunjungi
                    portal resmi SPMB Jawa Timur.
                </p>

                <a
                    href="#"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="mt-4 inline-flex items-center gap-2 rounded-lg bg-white px-4 py-2 text-sm font-medium text-[#1F2937] shadow-sm transition-colors duration-200 hover:bg-gray-50"
                >
                    <span
                        class="flex h-5 w-5 items-center justify-center rounded-full bg-[#3B82F6] text-xs text-white"
                    >
                        ⊕
                    </span>
                    Kunjungi portal resmi
                    <span class="font-semibold text-[#3B82F6]"
                        >SPMB Jawa Timur</span
                    >
                </a>
            </div>
        </div>
    </section>
</template>
