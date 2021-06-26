<template>
  <div>
    <button @click="click('asdasd')" class="button py-20 px-20">
      Test
    </button>
  </div>
</template>
<script>
export default {
  methods:{
    click(test){
      alert(test)
    }
  }
}
</script>