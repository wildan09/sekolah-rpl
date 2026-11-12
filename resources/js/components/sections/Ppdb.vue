<script setup>
import { Link } from '@inertiajs/vue3'

defineProps({
  heroImage: {
    type: String,
    default: '/images/ppdb-hero-bg.webp',
  },
  schoolLogo: {
    type: String,
    default: '/images/logo-sekolah.webp',
  },
})
</script>

<template>
  <section 
    class="relative w-full h-173.5 overflow-hidden flex items-center bg-cover bg-center bg-no-repeat"
    :style="{ backgroundImage: `url(${heroImage})` }"
  >
    
    <div class="absolute inset-0 bg-linear-to-r from-secondary-60 via-secondary-60/80 to-secondary-60/40 z-0"></div>

    <div class="w-full max-w-360 mx-auto flex flex-col-reverse lg:flex-row justify-between items-center px-27.5 sm:px-4 sm:pt-16.75 sm:pb-12.75 md:px-14 relative z-3">
      
      <div class="max-w-2xl w-full flex flex-col items-center lg:items-start text-center lg:text-left">
        <h2 class="heading-1 font-bold text-white leading-tight">
          Penerimaan Peserta Didik Baru
          <span class="text-primary-60">(PPDB)</span>
        </h2>

        <p class="mt-5 text-neutral-40 text-[24px] leading-[120%]">
          Siap bergabung dengan bagian SMK NEGERI 1 PURWOSARI? Akses portal
          resmi PPDB Pemerintah untuk melihat jadwal lengkap, persyaratan,
          serta pendaftaran secara online.
        </p>

        <Link
          href="/ppdb"
          class="mt-15 inline-flex items-center gap-5 rounded-xl bg-primary-60 px-5 py-2.5 font-semibold text-secondary-60 hover:bg-primary-50 transition-colors"
        >Lihat Selengkapnya
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M20.7806 12.531L14.0306 19.281C13.8899 19.4218 13.699 19.5008 13.5 19.5008C13.301 19.5008 13.1101 19.4218 12.9694 19.281C12.8286 19.1403 12.7496 18.9494 12.7496 18.7504C12.7496 18.5514 12.8286 18.3605 12.9694 18.2198L18.4397 12.7504H3.75C3.55109 12.7504 3.36032 12.6714 3.21967 12.5307C3.07902 12.3901 3 12.1993 3 12.0004C3 11.8015 3.07902 11.6107 3.21967 11.4701C3.36032 11.3294 3.55109 11.2504 3.75 11.2504H18.4397L12.9694 5.78104C12.8286 5.64031 12.7496 5.44944 12.7496 5.25042C12.7496 5.05139 12.8286 4.86052 12.9694 4.71979C13.1101 4.57906 13.301 4.5 13.5 4.5C13.699 4.5 13.8899 4.57906 14.0306 4.71979L20.7806 11.4698C20.8504 11.5394 20.9057 11.6222 20.9434 11.7132C20.9812 11.8043 21.0006 11.9019 21.0006 12.0004C21.0006 12.099 20.9812 12.1966 20.9434 12.2876C20.9057 12.3787 20.8504 12.4614 20.7806 12.531Z" fill="#132133"/>
          </svg>
        </Link>
      </div>

      <div class="w-48 h-48 sm:w-56 sm:h-56 lg:w-90 lg:h-90 shrink-0">
        <img
          :src="schoolLogo"
          alt="Logo SMK Negeri 1 Purwosari"
          class="w-full h-full object-contain"
        />
      </div>

    </div>
  </section>
</template>