<template>
  <HeaderComponent />
  <main class="container my-4">
    <router-view></router-view>
  </main>
</template>

<script>
  import HeaderComponent from './components/HeaderComponent.vue';
  import { store } from './store';
  import Axios from 'axios';
  export default {
    name: 'App',
    components: {
      HeaderComponent
    },
    data() {
      return {
        store,
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>