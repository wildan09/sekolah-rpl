<script setup>
const misiList = [
    "Mengembangkan pendidikan karakter dengan mengintegrasikan nilai-nilai Agama, nasionalisme dan budaya industri dalam Kurikulum Satuan Pendidikan.",
    "Mengembangkan pengetahuan, keterampilan, dan inovasi peserta didik sesuai bidangnya.",
    "Meningkatkan daya saing lulusan di tingkat regional, nasional dan internasional.",
    "Memberikan layanan pendidikan sesuai standar, tugas dan fungsi masing-masing dalam pergaulan sesama warga sekolah dalam suasana kekeluargaan.",
    "Mengembangkan kemitraan dengan masyarakat dan industri.",
    "Mengelola sarana dan prasarana sekolah untuk pengembangan budaya, pelatihan, produksi dan jasa berbasis teaching factory; dan pendidikan lingkungan hidup.",
    "Mengembangkan budaya sekolah untuk melestarikan fungsi lingkungan, mencegah pencemaran dan kerusakan lingkungan.",
];

const isLastAndOdd = (index) =>
    misiList.length % 2 !== 0 && index === misiList.length - 1;
</script>

<template>
    <div class="w-full px-4 py-6 sm:px-8 lg:px-27.5">
        <div
            class="mb-8 flex w-full flex-col justify-center gap-2.5 rounded-[20px] bg-[#FFF8E8] px-6 py-5 text-center transition-shadow duration-300 hover:shadow-md sm:px-10 lg:mb-10 lg:min-h-39 lg:px-10 lg:py-5"
        >
            <h2
                class="text-xl font-semibold text-[#1F2937] sm:text-2xl lg:text-3xl"
            >
                Visi
            </h2>
            <p
                class="w-full text-center text-base font-normal leading-[1.2] text-[#00000099] sm:text-lg lg:text-2xl"
            >
                “Mewujudkan SMK Yang Unggul, Berkarakter Dan Berdaya Saing
                Global Untuk Mendukung Jawa Timur Cerdas Yang Berkelanjutan”
            </p>
        </div>
        <h2
            class="mb-6 text-center text-xl font-semibold text-[#1F2937] sm:text-2xl lg:text-3xl"
        >
            Misi
        </h2>

        <div class="grid grid-cols-1 gap-4 md:grid-cols-2">
            <div
                v-for="(misi, index) in misiList"
                :key="index"
                :class="[
                    'flex cursor-default items-center gap-4 rounded-[10px] bg-white px-5 py-4 shadow-sm transition-all duration-300 ease-out hover:-translate-y-1 hover:shadow-lg',
                    isLastAndOdd(index) ? 'md:col-span-2' : '',
                ]"
            >
                <div
                    class="flex h-10 w-10 shrink-0 items-center justify-center rounded-full bg-[#FFD45C] text-lg font-semibold text-black transition-transform duration-300"
                >
                    {{ index + 1 }}
                </div>
                <p class="text-lg font-normal leading-[1.2] text-[#00000099]">
                    {{ misi }}
                </p>
            </div>
        </div>
    </div>
</template>
