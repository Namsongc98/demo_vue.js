<template>
  <div class="">
    <Header />
    <Body />
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header/Header.vue'
import Body from"./components/Body/Body.vue"
import Footer from './components/Footer/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    Body,
    Footer
  }
}
</script>

<style></style>
