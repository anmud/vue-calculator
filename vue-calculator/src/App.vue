<template>
  <div id="app">
    
    <app-calculator></app-calculator>


    
  </div>
</template>

<script>
import Calculator from '../src/components/Calculator'
export default {
  name: 'app',
  data () {
    return {
    
    }
  },
  components:{
    'app-calculator': Calculator,
  }
}
</script>

<style>

</style>
