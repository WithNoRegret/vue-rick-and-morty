<template>
  <MainHeader/>
  <main class="main">
    <RouterView/>
  </main>
  <MainFooter/>
</template>

<script>
import MainHeader from './components/MainHeader.vue'
import MainFooter from './components/MainFooter.vue';

export default {
  name: 'App',
  components: {
    MainHeader,
    MainFooter
  }
}
</script>

<style scoped>

.main {
  flex-grow: 1;
  padding: 20px;
}
</style>