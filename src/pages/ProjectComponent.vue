<template>
    <div v-if="project">
        <img :src="getImage" class="projectimg" :alt="project.title">
        <h1 class="my-4">{{ project.title }}</h1>
        <p>{{ project.content }}</p>
        <p>{{ project.technology ?.name }}</p>
        <!-- <RouterLink :to="{ name: 'single-project', params: { 'slug': 'eum-porro-sed-optio-quis-itaque-ex-harum' } }">Leggi
            altro articolo</RouterLink> -->
    </div>
</template>

<script>
import { store } from '../store';
    export default {
        name: 'ProjectComponent',
        data() {
            return {
                store
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>