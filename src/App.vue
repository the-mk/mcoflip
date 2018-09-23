<template>
  <div id="app">
    <TopHeader></TopHeader>
    <Spinner v-if="!isLoaded"></Spinner>
    <MainContent v-on:setChangedStatus="setChangedStatus"></MainContent>
  </div>
</template>

<script>
import Spinner from './components/Spinner.vue'
import MainContent from './components/MainContent.vue'
import TopHeader from './components/TopHeader.vue'

export default {
  name: 'app',
  components: {
    TopHeader,
    MainContent,
    Spinner
  },
  data () {
    return {
      success: false,
      isLoaded: false
    }
  },
  methods: {
    setChangedStatus (value) {
      this.$data[value] = true;
    }
  },
}
</script>

<style lang="scss">
html {
  background: url(https://www.toptal.com/designers/subtlepatterns/patterns/geometry2.png);
}
</style>
