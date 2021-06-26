<template>
  <div class="flex flex-col justify-center my-10">
    <loaderSect v-if="isLoad" />
    <div class="relative mx-10" v-else>
      <div class="relative px-4 py-10 bg-white shadow-lg p-10 rounded-xl">
        <div class="mx-auto">
          <div class="py-5 flex">
            <nuxt-link to="/" class="text-indigo-800 font-semibold flex-1"
              >🡠 Back to Home</nuxt-link
            >
            <a
              href="#Report"
              class="
                text-white
                inline-block
                bg-red-600
                hover:bg-red-800
                hover:text-red-200
                py-1
                px-5
                rounded-md
              "
              >Report Broken</a
            >
          </div>
          <h1 class="font-semiboldtext-gray-900 font-bold text-4xl">
            {{ item.Title }}
          </h1>
          <p class="font-light text-4x4 text-gray-600 pb-5">
            Updated on {{ getDate }}
          </p>
          <div v-if="item.Youtube" class="relative" style="padding-top: 56.25%">
            <iframe
              class="absolute inset-0 w-full h-full"
              height="315"
              :src="'https://www.youtube.com/embed/' + item.Youtube"
            >
            </iframe>
          </div>
          <div></div>
          <div class="divide-y divide-gray-200">
            <div
              class="
                py-8
                text-base
                leading-6
                space-y-4
                text-gray-700
                sm:text-lg
                sm:leading-7
              "
            >
              <div>
                <vue-simple-markdown
                  :source="item.Content"
                ></vue-simple-markdown>
              </div>
            </div>
            <slideshowComps :images="thumb" />
            <div class="pt-6 text-center pb-6">
              <p class="font-bold uppercase pb-5">Download Link</p>
              <p>
                <a
                v-if="item.Drive"
                  class="
                    py-2
                    px-4
                    rounded-lg
                    font-bold
                    text-white
                    hover:bg-green-600
                    bg-green-800
                    inline-flex
                    items-center
                  "
                  :href="item.Drive"
                >
                  <svg
                    class="fill-current w-4 h-4 mr-2"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                  >
                    <path d="M13 8V2H7v6H2l8 8 8-8h-5zM0 18h20v2H0v-2z" />
                  </svg>
                  <span>Google Drive</span>
                </a>
                <a
                v-if="item.Mega"
                  class="
                    bg-red-600
                    hover:bg-red-800
                    text-white
                    font-bold
                    py-2
                    px-4
                    rounded-lg
                    inline-flex
                    items-center
                  "
                  :href="item.Mega"
                >
                  <svg
                    class="fill-current w-4 h-4 mr-2"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                  >
                    <path d="M13 8V2H7v6H2l8 8 8-8h-5zM0 18h20v2H0v-2z" />
                  </svg>
                  <span>Mega Download</span>
                </a>
              </p>
            </div>
            <div v-if="isCategories" class="px-6 pt-4 pb-2">
            <div v-for="items in item.categories" :key="items.id">
              <nuxt-link
              :to="'/tag/'+items.Slug"
                class="
                  inline-block
                  bg-gray-200
                  rounded-full
                  px-3
                  py-1
                  text-sm
                  font-semibold
                  text-gray-700
                  mr-2
                  mb-2
                "
                >{{items.Label}}</nuxt-link
              >
            </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- jika Kosong -->
  </div>
</template>
<script>
import slideshowComps from '@/components/slideshowComps'
import loaderSect from '@/components/loaderSect'
export default {
  head() {
    return {
      title: this.item.Title + ' - 90Games',
      meta: [
        {
          hid: this.item.Excerpt,
          name:
            this.item.Excerpt +
            'Android private server download, download dragonnest private server' +
            this.year,
          content:
            this.item.Title +
            ', Android private server download, download dragonnest private server' +
            this.item.Excerpt +
            ' ' +
            this.year,
        },
        {
          property: 'og:title',
          content: `${this.item.Title}`,
        },
        {
          property: 'og:description',
          content: `${this.item.Content}`.replace(/<\/?[^>]+(>|$)/g, ''),
        },
        {
          property: 'og:image',
          content: `${this.picture}`,
        },
      ],
    }
  },
  data() {
    return {
      item: {
        Title:''
      },
      thumb:[],
      year: '2021',
      picture:'',
      isCategories: true,
      isLoad: true,
    }
  },
  components: {
    loaderSect,
    slideshowComps
  },
  async mounted() {
    var a = new Date()
    var b = a.getFullYear()
    this.year = b
    const res = await this.$axios.get(
      process.env.aplication+'?Slug=' + this.$route.params.slug
    )
    if (res.data.length !== 0) {
      this.isLoad = false
      this.picture = process.env.baseURL + res.data[0].Cover[0].formats.medium.url
      this.thumb = res.data[0].Cover
      this.item = res.data[0]
      if (res.data[0].categories.length == 0) {
        this.isCategories = false
      } else {
        this.isCategories = true
      }
    } else {
      this.$router.push('/404')
    }
  },
  computed: {
    getDate() {
      return this.$moment(this.item.update, 'YYYY-MM-DD').fromNow()
    },
  },
}
</script>