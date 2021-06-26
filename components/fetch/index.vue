<template>
  <div
    class="
      mx-5
      my-5
      overflow-hidden
      bg-white
      rounded-lg
      shadow-lg
      dark:bg-gray-800
      transform
      hover:scale-120
    "
  >
    <img
      class="object-cover w-full h-56"
      @click="url"
      :src="img"
      :alt="judul"
    />

    <div class="py-5 text-center"  @click="url">
      <p
        class="block text-md font-bold text-gray-800 dark:text-white px-2"
        >{{judul}}</p
      >
      <span class="text-sm text-gray-700 dark:text-gray-200"
        >Size {{size}} MB</span
      >
    </div>
  </div>
</template>
<script>
export default {
  data(){
    return {
      urlBase: process.env.baseURL
    }
  },
  props: ['judul','size','img','to'],
  methods:{
      url(){
          this.$router.push('/detail/'+this.to)
      }
  }
}
</script>