<template>
    <div
        class="flex h-12 w-full max-w-175 justify-end overflow-hidden transition-all duration-1000 ease-in-out"
    >
        <input
            type="text"
            placeholder="Search..."
            class="h-12 min-w-0 flex-1 border border-gray-300 bg-white px-4 text-sm text-gray-700 outline-none placeholder:text-gray-400 transition-all duration-1000 ease-in-out focus:border-gray-400 max-sm:w-0 max-sm:flex-none max-sm:px-0 max-sm:opacity-0"
        />
        <button
            type="button"
            class="flex h-12 w-13 shrink-0 items-center justify-center bg-[#252525] transition-all duration-1000 ease-in-out hover:bg-[#111111] max-sm:h-12 max-sm:w-12 max-sm:rounded-full"
        >
            <img
                src="/icons/search.png"
                alt="Search"
                class="h-5 w-5 object-contain"
            />
        </button>
    </div>
</template>
