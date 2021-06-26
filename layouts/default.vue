<template>
  <div>
    <NavbarComponent :title="title"/>
    <div class="exclude">
      <searchSect />
    <Nuxt keep-alive />
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
    }
  },
}
</script>
<style>
.exclude{
  margin-top: 0;
  background-image: url('@/assets/img/background.svg');
  background-size: cover;
  background-repeat: no-repeat;
  height: 100%;
  width: auto;
  
}
</style>