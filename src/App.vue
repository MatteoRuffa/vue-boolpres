<template>
  <HeaderComponent />
  <main class="container my-4">
    <router-view></router-view>
  </main>
</template>

<script>
  import HeaderComponent from './components/HeaderComponent.vue';
  import { store } from './store';
  import axios from 'axios';
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
    methods: {
    getTechnologies() {
        axios.get(this.store.apiBaseUrl + '/technologies').then((res) => {
          // console.log(res.data);
          this.store.technologies = res.data.results;
        });
      }
    },
    mounted() {
      this.getTechnologies();
    }
  }
</script>

<style lang="scss" scoped>

</style>