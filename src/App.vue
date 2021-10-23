<template>
  <TheHeader />
  <main class="container">
    <router-view/>
  </main>
</template>

<script>
import TheHeader from './components/TheHeader.vue'
import './assets/style/normalize.css'
import './assets/style/global.css'

export default {
  components: {
    TheHeader
  }
}
</script>

<style lang="scss">
</style>
