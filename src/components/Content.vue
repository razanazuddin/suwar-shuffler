<template>
  <div id="suwarSection" class="h-48 flex items-center justify-center mx-auto">
    <div class="text-center py-4 space-y-3">
      <h2 class="text-6xl font-extrabold">{{ quranMeta[state.startIndex].name }}</h2>
      <p>{{ quranMeta[state.startIndex].tname }}</p>
      <small>{{ quranMeta[state.startIndex].ename }}</small>
    </div>
  </div>
  <div id="shufflerSection" class="space-y-3">
    <div id="shufflerButton">
      <button
        class="border rounded-lg w-72 h-32 bg-amber-500 hover:bg-amber-600 text-4xl text-white tracking-wider font-extrabold uppercase"
        @click="shuffleSuwar"
      >
        Shuffle!
      </button>
    </div>
    <div id="shufflerSettings" class="flex items-center justify-between">
        <p>Pick a surah from</p>
        <div class="relative inline-block text-left">
          <button
            type="button"
            class="inline-flex w-full justify-center rounded-md border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 shadow-sm hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:ring-offset-gray-100"
            @click="state.toggleDropdown = !state.toggleDropdown"
          >
            {{ state.selectedDivision }}
            <svg class="-mr-1 ml-2 h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
              <path fill-rule="evenodd" d="M5.23 7.21a.75.75 0 011.06.02L10 11.168l3.71-3.938a.75.75 0 111.08 1.04l-4.25 4.5a.75.75 0 01-1.08 0l-4.25-4.5a.75.75 0 01.02-1.06z" clip-rule="evenodd" />
            </svg>
          </button>
          <div v-if="state.toggleDropdown" class="absolute right-0 z-10 mt-2 w-56 origin-top-right rounded-md bg-white shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none" role="menu" aria-orientation="vertical" aria-labelledby="menu-button" tabindex="-1">
            <div class="py-1" role="none">
              <div v-for="(division, i) in quranDivision" :key="i" :value="division" href="#" :class="[division === state.selectedDivision ? 'bg-gray-100 text-gray-900' : 'text-gray-700 cursor-pointer', 'block px-4 py-2 text-sm']" role="menuitem" tabindex="-1" @click="state.selectedDivision = division; state.toggleDropdown = false;">{{ division }}</div>
            </div>
          </div>
        </div>
    </div>
  </div>
</template>

<script>
import { reactive } from '@vue/reactivity';
import data from '../assets/quran-meta.json'
export default {
  props: {
    msg: String
  },
  setup() {
    const quranMeta = data['quran-meta'];
    const quranDivision = [
      'All',
      'The Three',
      'The Five',
      'The Seven',
      'The Nine',
      'The Eleven',
      'The Thirteen',
      'Al-Mufassal',
    ]
    const state = reactive({
      startIndex: 0,
      selectedDivision: 'All',
      toggleDropdown: false
    });

    function shuffleSuwar() {
      if (state.selectedDivision !== 'All') {
        const filteredQuranMeta = quranMeta.filter((meta) => meta.division === state.selectedDivision);
        const filteredStartIndex = Math.floor(Math.random() * filteredQuranMeta.length);
        const filteredSurah = filteredQuranMeta[filteredStartIndex];
        state.startIndex = quranMeta.findIndex((meta) => filteredSurah.index === meta.index);
      } else {
        state.startIndex = Math.floor(Math.random() * quranMeta.length);
      }
    }
    return {
      state,
      shuffleSuwar,
      quranMeta,
      quranDivision
    }
  }
}
</script>
