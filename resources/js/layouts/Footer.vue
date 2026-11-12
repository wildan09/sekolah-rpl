<script setup>
import { Link } from '@inertiajs/vue3'

const navigasi = [
  { label: 'Beranda', href: '/' },
  { label: 'Profil', href: '/profil' },
  { label: 'Layanan', href: '/layanan' },
  { label: 'Berita', href: '/berita' },
  { label: 'PPDB', href: '/ppdb' },
  { label: 'BLUD', href: '/blud' },
]

const socials = [
  { name: 'Instagram', href: 'https://instagram.com/smkn1purwosari' },
  { name: 'Facebook', href: 'https://facebook.com/smkn1purwosari' },
  { name: 'Youtube', href: 'https://youtube.com/@smkn1purwosari' },
  { name: 'TikTok', href: 'https://tiktok.com/@smkn1purwosari' },
]

const year = new Date().getFullYear()

function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>

<template>
  <footer class="relative overflow-hidden bg-secondary-60 text-neutral-40">
    <div class="w-full pointer-events-none absolute left-1/2 bottom-0 h-28 w-2/3 -translate-x-1/2 translate-y-1/2 rounded-full bg-[radial-gradient(closest-side,_#FFC107_0%,_transparent_100%)] opacity-90 blur-1xl"></div>
    <div class="relative z-10 mx-auto max-w-[1440px] px-8 py-8 sm:px-[32px] sm:pt-[67px] sm:pb-[51px] md:px-[56px] lg:px-[110px]">
      <div class="grid grid-cols-1 gap-y-6 sm:grid-cols-2 sm:gap-x-[40px] sm:gap-y-[40px] lg:grid-cols-[2fr_0.5fr_1fr_1.5fr] lg:gap-x-[68px]">

        <div class="max-w-[380px]">
          <div class="flex items-center gap-3">
            <img
              src="/images/logo-sekolah.png"
              alt="Logo SMK Negeri 1 Purwosari"
              class="h-[69px] w-[71px] shrink-0 object-contain"
            />
            <h3 class="font-poppins text-xl font-bold text-white leading-tight">
              SMK NEGERI 1<br />PURWOSARI
            </h3>
          </div>

          <p class="mt-8.5 text-lg leading-relaxed">
            Pusat pendidikan kejuruan yang unggul dan berkomitmen mencetak
            lulusan kompeten, berkarakter, berjiwa wirausaha, serta siap
            bersaing didunia kerja.
          </p>

          <div class="max-w-[380px] mt-8.5 flex gap-3">
            <a
              v-for="social in socials"
              :key="social.name"
              :href="social.href"
              target="_blank"
              rel="noopener noreferrer"
              :aria-label="social.name"
              class="flex h-9 w-9 items-center justify-center border border-secondary-50 rounded-full text-white transition-colors hover:bg-primary-50 hover:text-secondary-90"
            >
              <!-- Instagram -->
              <svg v-if="social.name === 'Instagram'" viewBox="0 0 24 24" class="h-4 w-4" fill="currentColor">
                <path d="M12 2c2.7 0 3.06.01 4.12.06 1.06.05 1.79.22 2.43.47.66.26 1.22.6 1.77 1.15.55.55.9 1.11 1.15 1.77.25.64.42 1.37.47 2.43.05 1.06.06 1.42.06 4.12s-.01 3.06-.06 4.12c-.05 1.06-.22 1.79-.47 2.43a4.9 4.9 0 0 1-1.15 1.77 4.9 4.9 0 0 1-1.77 1.15c-.64.25-1.37.42-2.43.47-1.06.05-1.42.06-4.12.06s-3.06-.01-4.12-.06c-1.06-.05-1.79-.22-2.43-.47a4.9 4.9 0 0 1-1.77-1.15 4.9 4.9 0 0 1-1.15-1.77c-.25-.64-.42-1.37-.47-2.43C2.01 15.06 2 14.7 2 12s.01-3.06.06-4.12c.05-1.06.22-1.79.47-2.43.26-.66.6-1.22 1.15-1.77A4.9 4.9 0 0 1 5.45 2.53c.64-.25 1.37-.42 2.43-.47C8.94 2.01 9.3 2 12 2Zm0 1.8c-2.65 0-2.98.01-4.02.06-.86.04-1.33.18-1.64.3-.41.16-.7.35-1.01.66-.31.31-.5.6-.66 1.01-.12.31-.26.78-.3 1.64C4.31 9.02 4.3 9.35 4.3 12s.01 2.98.06 4.02c.04.86.18 1.33.3 1.64.16.41.35.7.66 1.01.31.31.6.5 1.01.66.31.12.78.26 1.64.3 1.04.05 1.37.06 4.02.06s2.98-.01 4.02-.06c.86-.04 1.33-.18 1.64-.3.41-.16.7-.35 1.01-.66.31-.31.5-.6.66-1.01.12-.31.26-.78.3-1.64.05-1.04.06-1.37.06-4.02s-.01-2.98-.06-4.02c-.04-.86-.18-1.33-.3-1.64a2.7 2.7 0 0 0-.66-1.01 2.7 2.7 0 0 0-1.01-.66c-.31-.12-.78-.26-1.64-.3C14.98 3.81 14.65 3.8 12 3.8Zm0 3.06a5.14 5.14 0 1 1 0 10.28 5.14 5.14 0 0 1 0-10.28Zm0 1.8a3.34 3.34 0 1 0 0 6.68 3.34 3.34 0 0 0 0-6.68Zm5.34-1.98a1.2 1.2 0 1 1-2.4 0 1.2 1.2 0 0 1 2.4 0Z"/>
              </svg>
              <!-- Facebook -->
              <svg v-else-if="social.name === 'Facebook'" viewBox="0 0 24 24" class="h-4 w-4" fill="currentColor">
                <path d="M13.5 21v-7.9h2.65l.4-3.08H13.5V8.06c0-.89.25-1.5 1.53-1.5h1.63V3.8A22 22 0 0 0 14.3 3.7c-2.31 0-3.9 1.41-3.9 4v2.32H7.75v3.08h2.65V21h3.1Z"/>
              </svg>
              <!-- YouTube -->
              <svg v-else-if="social.name === 'Youtube'" viewBox="0 0 24 24" class="h-4 w-4" fill="currentColor">
                <path d="M21.6 7.2s-.21-1.5-.87-2.16c-.83-.87-1.76-.87-2.19-.92C15.44 3.9 12 3.9 12 3.9h-.01s-3.44 0-6.54.22c-.43.05-1.36.05-2.19.92C2.6 5.7 2.4 7.2 2.4 7.2S2.18 8.95 2.18 10.7v1.6c0 1.75.22 3.5.22 3.5s.21 1.5.86 2.16c.83.87 1.92.84 2.4.94 1.75.17 7.44.22 7.44.22s3.45-.01 6.55-.23c.43-.05 1.36-.05 2.19-.92.65-.66.87-2.16.87-2.16s.22-1.75.22-3.5v-1.6c0-1.75-.22-3.5-.22-3.5ZM9.98 14.3V8.7l5.6 2.81-5.6 2.8Z"/>
              </svg>
              <!-- TikTok -->
              <svg v-else viewBox="0 0 24 24" class="h-4 w-4" fill="currentColor">
                <path d="M16.5 3h-2.7v11.6a2.7 2.7 0 1 1-1.9-2.58V8.9a5.4 5.4 0 1 0 4.6 5.34V9.3a6.5 6.5 0 0 0 3.9 1.3V7.9a3.8 3.8 0 0 1-3.9-3.9V3Z"/>
              </svg>
            </a>
          </div>
        </div>

        <!-- Navigasi -->
        <div class="max-w-[84px]">
          <h4 class="text-base font-bold text-white text-[22px]">Navigasi</h4>
          <ul class="mt-6 space-y-3 text-base text-neutral-40">
            <li v-for="item in navigasi" :key="item.label">
              <Link :href="item.href" class="transition-colors hover:text-primary-50">
                {{ item.label }}
              </Link>
            </li>
          </ul>
        </div>

        <div>
          <h4 class="text-base font-bold text-white text-[22px]">Kontak Kami</h4>
          <ul class="mt-6 space-y-4 text-base text-neutral-40">
            <li class="flex items-start gap-3">
              <svg width="30" height="30" viewBox="0 0 30 30" fill="none" xmlns="http://www.w3.org/2000/svg">
                <g clip-path="url(#clip0_1093_6921)">
                <path d="M17.25 7.5C18.5114 7.83218 19.6621 8.4932 20.5844 9.41557C21.5068 10.3379 22.1678 11.4886 22.5 12.75" stroke="#FFC107" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M16.5 10.5C18.0488 10.9144 19.0856 11.9512 19.5 13.5" stroke="#FFC107" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M17.6616 17.3752C17.7654 17.3061 17.8849 17.264 18.0091 17.2527C18.1334 17.2414 18.2585 17.2613 18.3731 17.3106L22.7944 19.2915C22.9434 19.3552 23.0677 19.4654 23.1489 19.6057C23.23 19.7459 23.2635 19.9087 23.2444 20.0696C23.0987 21.1581 22.5627 22.1566 21.736 22.8795C20.9093 23.6024 19.8482 24.0005 18.75 23.9996C15.3685 23.9996 12.1255 22.6563 9.73439 20.2652C7.3433 17.8741 6 14.6311 6 11.2496C5.99916 10.1514 6.3972 9.09032 7.12009 8.26361C7.84298 7.43691 8.84152 6.90089 9.93 6.75524C10.0909 6.73612 10.2537 6.76963 10.3939 6.85075C10.5342 6.93187 10.6444 7.05624 10.7081 7.20524L12.6891 11.6302C12.7377 11.7439 12.7576 11.8678 12.7468 11.991C12.736 12.1141 12.6949 12.2327 12.6272 12.3362L10.6238 14.7184C10.5527 14.8256 10.5107 14.9494 10.5018 15.0778C10.4929 15.2061 10.5175 15.3346 10.5731 15.4506C11.3484 17.0377 12.9891 18.6587 14.5809 19.4265C14.6975 19.4819 14.8266 19.5059 14.9553 19.4962C15.084 19.4865 15.208 19.4434 15.315 19.3712L17.6616 17.3752Z" stroke="#FFC107" stroke-linecap="round" stroke-linejoin="round"/>
                </g>
                <defs>
                <clipPath id="clip0_1093_6921">
                <rect width="24" height="24" fill="white" transform="translate(3 3)"/>
                </clipPath>
                </defs>
            </svg>

              <div>
                <p class="text-sm text-neutral-40">Call Us</p>
                <p class="text-white text-base">(0343) 613747</p>
              </div>
            </li>
            <li class="flex items-start gap-3">
              <svg width="30" height="30" viewBox="0 0 30 30" fill="none" xmlns="http://www.w3.org/2000/svg">
                <g clip-path="url(#clip0_1093_6931)">
                <path d="M6 8.25H24V21C24 21.1989 23.921 21.3897 23.7803 21.5303C23.6397 21.671 23.4489 21.75 23.25 21.75H6.75C6.55109 21.75 6.36032 21.671 6.21967 21.5303C6.07902 21.3897 6 21.1989 6 21V8.25Z" stroke="#FFC107" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M24 8.25L15 16.5L6 8.25" stroke="#FFC107" stroke-linecap="round" stroke-linejoin="round"/>
                </g>
                <defs>
                <clipPath id="clip0_1093_6931">
                <rect width="24" height="24" fill="white" transform="translate(3 3)"/>
                </clipPath>
                </defs>
            </svg>

              <div>
                <p class="text-sm text-neutral-40">Mail Us</p>
                <p class="text-white text-base">informasi@smkn1purwosari.sch.id</p>
              </div>
            </li>
            <li class="flex items-start gap-3">
              <svg width="30" height="30" viewBox="0 0 30 30" fill="none" xmlns="http://www.w3.org/2000/svg">
                <g clip-path="url(#clip0_1093_6940)">
                <path d="M15 15.75C16.6569 15.75 18 14.4069 18 12.75C18 11.0931 16.6569 9.75 15 9.75C13.3431 9.75 12 11.0931 12 12.75C12 14.4069 13.3431 15.75 15 15.75Z" stroke="#FFC107" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M22.5 12.75C22.5 19.5 15 24.75 15 24.75C15 24.75 7.5 19.5 7.5 12.75C7.5 10.7609 8.29018 8.85322 9.6967 7.4467C11.1032 6.04018 13.0109 5.25 15 5.25C16.9891 5.25 18.8968 6.04018 20.3033 7.4467C21.7098 8.85322 22.5 10.7609 22.5 12.75Z" stroke="#FFC107" stroke-linecap="round" stroke-linejoin="round"/>
                </g>
                <defs>
                <clipPath id="clip0_1093_6940">
                <rect width="24" height="24" fill="white" transform="translate(3 3)"/>
                </clipPath>
                </defs>
            </svg>
              <div>
                <p class="text-sm text-neutral-40">Office Address</p>
                <p class="text-white text-base">www.smkn1purwosari.sch.id</p>
              </div>
            </li>
          </ul>
        </div>

        <div>
          <div class="aspect-video w-full overflow-hidden rounded-xl bg-neutral-10/10">
            <iframe
              src="https://www.google.com/maps?q=SMK+Negeri+1+Purwosari&output=embed"
              class="h-full w-full border-0"
              loading="lazy"
              referrerpolicy="no-referrer-when-downgrade"
              title="Lokasi SMK Negeri 1 Purwosari"
            />
          </div>
          <a
            href="https://www.google.com/maps?q=SMK+Negeri+1+Purwosari"
            target="_blank"
            rel="noopener noreferrer"
            class="mt-2 flex items-center justify-center gap-2 rounded-lg bg-[#203958] py-2.5 text-sm text-white font-medium transition-colors hover:bg-secondary-50"
          >
            <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M12.9513 13.1062C14.1925 13.675 15 14.59 15 15.625C15 17.35 12.7625 18.75 10 18.75C7.2375 18.75 5 17.35 5 15.625C5 14.59 5.80625 13.675 7.0475 13.1062L7.38125 13.5487C7.94875 14.29 8.48875 14.9987 8.96625 15.7025C9.08087 15.8711 9.23498 16.0091 9.41517 16.1044C9.59535 16.1998 9.79613 16.2497 10 16.2497C10.2039 16.2497 10.4047 16.1998 10.5848 16.1044C10.765 16.0091 10.9191 15.8711 11.0337 15.7025C11.5423 14.9702 12.0708 14.252 12.6188 13.5487L12.9513 13.1062Z" fill="#FFC107"/>
                <path d="M10 1.25C13 1.25 15 3.215 15 6.16125C15 8.73375 12.7125 11.3075 10.8 13.8812C10.5255 14.2485 10.2587 14.6215 10 15C9.4775 14.23 8.8875 13.46 8.29875 12.6888C6.63625 10.5138 5 8.3375 5 6.1625C5 3.215 7 1.25 10 1.25ZM10 3.705C9.3375 3.705 8.70125 3.965 8.2325 4.425C8.00129 4.65131 7.81744 4.92138 7.69168 5.21948C7.56592 5.51757 7.50076 5.83772 7.5 6.16125C7.5 6.81125 7.7625 7.43625 8.2325 7.89625C8.70125 8.3575 9.3375 8.61625 10 8.61625C10.6625 8.61625 11.2987 8.3575 11.7675 7.89625C11.9988 7.67037 12.1826 7.40052 12.3081 7.10256C12.4336 6.8046 12.4983 6.48456 12.4983 6.16125C12.4983 5.83794 12.4336 5.5179 12.3081 5.21994C12.1826 4.92198 11.9988 4.65213 11.7675 4.42625C11.2954 3.9638 10.6608 3.70486 10 3.705Z" fill="#FFC107"/>
            </svg>
            Lihat di Google Maps
          </a>
        </div>
      </div>

      <div class="mt-[137px] flex flex-col items-center justify-between gap-4 border-t border-neutral-40 pt-6 text-xs text-neutral-40 sm:flex-row">
        <p>© {{ year }} SMK Negeri 1 Purwosari. All rights reserved.</p>
        <button
          type="button"
          @click="scrollToTop"
          class="flex items-center gap-2 transition-colors hover:text-primary-50"
        >
          Back To Top
          <span class="flex h-8 w-8 items-center justify-center rounded-full bg-primary-50 text-white">
            <svg width="10" height="12" viewBox="0 0 10 12" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M5 11L5 1M9 5L5 1L1 5" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </span>
        </button>
      </div>
    </div>

  </footer>
</template>