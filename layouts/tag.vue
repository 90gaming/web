<template>
  <div>
    <NavbarComponent :title="title"/>
    <div class="exclude">
    <Nuxt />
    <footerSect :title="title"/>
    </div>
  </div>
</template>
<script>
import searchSect from '@/components/searchSect' 
import footerSect from '@/components/footerSect'
import NavbarComponent from '@/components/navbarComponent'
export default {
  components:{
    NavbarComponent,
    footerSect,
    searchSect
  },
  data(){
    return{
      title: '90Games',
      year: '',
    }
  },
  mounted(){
    var a  = new Date()
    var b = a.getFullYear()
    this.year = b
  }
}
</script>
<style>
.exclude{
  background-image: url('@/assets/img/background.svg');
  background-size: cover;
  
  
}
</style>