<template>
  <main>
    <div class="font-semibold text-3xl my-5 mx-5 text-gray-600">
      Tag : <span class="text-black">{{ $route.params.slug }}</span>
    </div>
    <div v-if="notFound" class="mx-auto">
        <p class="text-center font-semibold text-6xl mb-60">{{ $route.params.slug }} <span class="text-red-800">Not Found</span></p>
    </div>
    <loaderSect v-if="isLoad" />
    <div v-else class="grid grid-cols-2 md:grid-cols-4">
      <!-- COL -->

      <fetchData
        v-for="link in links"
        :key="link.id"
        :judul="link.Title"
        :img="urlImg + link.Cover[0].formats.small.url"
        :size="link.Size"
        :to="link.Slug"
      />

      <!-- END COL -->
    </div>
    <scrollingLoader v-if="isLoadFetch" />
  </main>
</template>
<script>
import scrollingLoader from '@/components/loaderScroll'
import fetchData from '@/components/fetch'
export default {
  head() {
    return {
      title: '90Games - Search: ' + this.$route.params.slug,
      meta: [
        {
          hid: 'Download android Private server ',
          name:
            'Android private server download '+ this.$route.params.slug+', download dragonnest private server' +
            this.year,
          content:
            'Android private server download '+ this.$route.params.slug+', download dragonnest private server' +
            this.year,
        },
      ],
    }
  },
  data() {
    return {
      urlImg: process.env.baseURL,
      isLoad: true,
      notFound: false,
      categories:{
        label: ''
      },
      page:1,
      isLoadFetch: false,
      links: [],
    }
  },
  components: {
    scrollingLoader,
    fetchData,
  },
  methods: {
    async getFetchApk() {
      const response = await this.$axios.get(process.env.aplication+`?Title_contains=` +this.$route.params.slug +`&_limit=8`)
      if(response.data.length !== 0){
          this.links = response.data
      }
      else{
          this.notFound = true
      }
      this.isLoad = false
    },
    getNextFetch() {
      this.isLoadFetch = true
      window.onscroll = () => {
        let bottomOfWindow =
          document.documentElement.scrollTop + window.innerHeight ===
          document.documentElement.offsetHeight
        if (bottomOfWindow) {
          this.page += 8
          const page = this.page
          this.$axios
            .get(process.env.aplication+`?Title_contains=` +
            this.$route.params.slug +`&_start=` + page + `&_limit=8`)
            .then((response) => {
              for (var i = 0; i < response.data.length; i++) {
                this.links.push(response.data[i])
              }
            })
        }
      }
       this.isLoadFetch = false
    },
  },
  beforeMount() {
    this.getFetchApk()
  },
  mounted(){
    this.getNextFetch()
  },
  async created(){
    
  }
}
</script>