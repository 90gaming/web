<template>
  <main class="mx-5 bg-white rounded-lg px-5 py-10 mb-20">
    <div class="mb-5">
      <p class="font-semibold text-6xl">{{datax.Title}}</p>
    </div>
    <div>
      <vue-simple-markdown :source="datax.Content"></vue-simple-markdown>
    </div>
  </main>
</template>
<script>
export default {
    data(){
        return{
            datax:{}
        }
    },
    async mounted(){
        const res = await this.$axios.get(process.env.about)
        this.datax = res.data
    }
}
</script>