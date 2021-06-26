<template>
  <main>
    <div class="font-semibold text-3xl my-5 mx-5 text-gray-600">
      Tag : <span class="text-black">{{ categories.Label }}</span>
    </div>
    <div v-if="isErrorFetch" class="mx-auto">
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
  layout: 'slug',
  head() {
    return {
      title: '90Games - Tag: ' + this.categories.Label,
      meta: [
        {
          hid: 'Download android Private server',
          name:
            'Android private server download '+ this.categories.Label+', download dragonnest private server' +
            this.year,
          content:
            'Android private server download '+ this.categories.Label+', download dragonnest private server' +
            this.year,
        },
      ],
    }
  },
  data() {
    return {
      isErrorFetch: false,
      urlImg: process.env.baseURL,
      isLoad: true,
      categories:{
        Label: ''
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
      const response = await this.$axios.get(process.env.aplication+`?categories.Slug=` +this.$route.params.slug +`&_limit=8`)
      if(response.data.length > 0){
        this.links = response.data
        this.isLoad = false
      }
      else{
        this.isErrorFetch = true
      }
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
            .get(process.env.aplication+`?categories.Slug=` +
            this.$route.params.slug +`&_start=` + page + `&_limit=8`)
            .then((response) => {
              for (var i = 0; i < response.data.length; i++) {
                this.links.push(response.data[i])
              }
              this.isLoadFetch = false
            })
        }
      }
    },
  },
  beforeMount() {
    this.getFetchApk()
  },
  mounted(){
    this.getNextFetch()
  },
  async created(){
    const rest = await this.$axios.get(process.env.categories+'?Slug='+this.$route.params.slug)
    if(rest.data.length > 0){
      this.categories = rest.data[0]
    }
    else{
      this.$router.push('/404')
    }
  }
}
</script>