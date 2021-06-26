<template>
  <header class="bg-gray-900 sm:flex sm:justify-between sm:items-center sm:px-4 sm:py-3">
    <div class="flex items-center justify-between px-4 py-3 sm:p-0">
      <div>
        <a href="" class="focus:bg-red-200">
        <img class="h-8 animate-pulse" src="~/assets/img/icon.svg" alt="Workcation">
        </a>
      </div>
      <a href="#" class="block px-2 py-1 text-white font-semibold rounded hover:text-indigo-200">90Games</a>
      <div class="sm:hidden">
        <button @click="isOpen = !isOpen" type="button" class="block text-gray-500 hover:text-white focus:text-white focus:outline-none">
          <svg class="h-6 w-6 fill-current" viewBox="0 0 24 24">
            <path v-if="isOpen" fill-rule="evenodd" d="M18.278 16.864a1 1 0 0 1-1.414 1.414l-4.829-4.828-4.828 4.828a1 1 0 0 1-1.414-1.414l4.828-4.829-4.828-4.828a1 1 0 0 1 1.414-1.414l4.829 4.828 4.828-4.828a1 1 0 1 1 1.414 1.414l-4.828 4.829 4.828 4.828z"/>
            <path v-if="!isOpen" fill-rule="evenodd" d="M4 5h16a1 1 0 0 1 0 2H4a1 1 0 1 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2z"/>
          </svg>
        </button>
      </div>
    </div>
    <nav :class="isOpen ? 'block' : 'hidden'" class="px-2 pt-2 pb-4 sm:flex sm:p-0">
      <nuxt-link to="/" exact-active-class="font-semibold bg-indigo-800" class="block px-2 py-1 text-white rounded hover:text-indigo-100 hover:bg-indigo-800">Home</nuxt-link>
      <dropdown/>
      <nuxt-link to="/about" exact-active-class="font-semibold bg-indigo-800"  class="mt-1 block px-2 py-1 text-white rounded hover:text-indigo-100 hover:bg-indigo-800 sm:mt-0 sm:ml-2">About</nuxt-link>
      <a href="https://www.youtube.com/channel/UC74wBbfujHBuGqCccsSzJBQ" target="_blank" class="mt-1 block px-2 py-1 text-white rounded hover:text-red-100 hover:bg-red-800 sm:mt-0 sm:ml-2">Youtube</a>
    </nav>
  </header>
</template>

<script>
import dropdown from '@/components/dropdown'
export default {
  components: {
    dropdown,
  },
  data() {
    return {
      isOpen: false,
    }
  },
}
</script>