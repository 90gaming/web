<template>
  <main>
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
    <scrollingLoader v-if="isLoadFetch"/>
  </main>
</template>
<script>
import scrollingLoader from '@/components/loaderScroll'
import loaderSect from '@/components/loaderSect'
import fetchData from '@/components/fetch'
export default {
  head(){
    return{
      title: '90Games - List Private Server Android',
      meta:[
        {
          hid: 'list pribate server android, Download android Private server '+ this.year,
          name: 'list pribate server android, Android private server download, download dragonnest private server'+ this.year,
          content: 'list pribate server android, Android private server download, download dragonnest private server'+ this.year,
        }
      ]
    }
  },
  data() {
    return {
      urlImg: process.env.baseURL,
      links: [],
      isLoad: true,
      isLoadFetch: false,
      page: 1,
    }
  },
  components: {
    fetchData,
    loaderSect,
    scrollingLoader
  },
  methods: {
    getFetchApk() {
      this.$axios
        .get(process.env.aplication+`?_limit=8`)
        .then((response) => {
          this.links = response.data
          this.isLoad = false
        })
    },
    getNextFetch() {
      this.isLoadFetch=true
      window.onscroll = () => {
        let bottomOfWindow =
          document.documentElement.scrollTop + window.innerHeight ===
          document.documentElement.offsetHeight
        if (bottomOfWindow) {
          this.page += 8
          const page = this.page
          this.$axios
            .get(
              process.env.aplication+`?_start=` +
                page +
                `&_limit=8`
            )
            .then((response) => {
              for(var i = 0; i < response.data.length; i++){
                 this.links.push(response.data[i])
              }
              this.isLoadFetch=false
            })
        }
      }
    },
  },
  beforeMount() {
    this.getFetchApk()
  },
  mounted() {
    this.getNextFetch()
  },
}
</script>