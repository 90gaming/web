<template>
  <div class="relative">
    <a @click="isOpen = !isOpen" class="mt-1 block px-2 py-1 text-white rounded hover:text-indigo-100 hover:bg-indigo-800 sm:mt-0 sm:ml-2" href="#">
     Categories <span style="display:inline-block;" class="animate-bounce">▼</span>
    </a>
    <a v-if="isOpen" @click="isOpen = false" tabindex="-1" class="fixed inset-0 h-full w-full bg-black opacity-50 cursor-default"></a>
    <div v-if="isOpen" class="absolute left-0 mt-2 py-2 w-48 bg-white rounded-lg shadow-xl">
      <nuxt-link class="block px-4 py-2 text-gray-800 hover:bg-indigo-500 hover:text-white" v-for="tag in tags" :key="tag.id" :to="'/tag/'+tag.Slug">{{tag.Label}}</nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isOpen: false,
      tags:[]
    }
  },
  async mounted() {
    const res = await this.$axios.get(process.env.categories) 
    this.tags = res.data
  },
}
</script>