<script setup>
const image = 'https://via.placeholder.com/176'
const name = 'Dr. Hj. Nining Faridah, M.Si.'
const position = 'Ka. KOMLI RPL'
</script>

<template>
  <div class="w-[380px] max-w-full rounded-[16px] bg-white shadow-[0_0_18px_0_rgba(0,0,0,0.05)] p-[32px] flex flex-col items-center gap-[40px]">
    <div class="h-28 w-28 rounded-full overflow-hidden bg-neutral-20 shrink-0">
      <img 
        :src="image" 
        :alt="name" 
        class="h-full w-full object-cover object-center"
      />
    </div>

    <div class="flex flex-col items-center text-center w-full">
      <h3 class="text-[22px] font-bold text-secondary-60">
        {{ name }}
      </h3>

      <p class="font-regular text-neutral-40 text-lg mt-[8px]">
        {{ position }}
      </p>

      <div v-if="$slots.footer" class="pt-4 mt-4 border-t border-neutral-20 w-full">
        <slot name="footer" />
      </div>
    </div>
  </div>
</template>