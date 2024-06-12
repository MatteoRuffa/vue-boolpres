<template>
    <div class="card mb-3" @click="openModal(item)">
        <div class="row g-0">
            <div class="col-md-8">
                <div class="card-body">
                    <h5 class="card-title"><strong>Title:</strong> {{ item.title }}</h5>
                    <p class="card-text"><strong>Description:</strong> {{ item.description }}</p>
                    <p class="card-text"><small class="text-body-secondary"><strong>Last updated:</strong>{{ item.updated_at }}</small></p>
                    <div v-if="item.technologies" class="d-flex flex-wrap align-items-center">
                        <strong>Technologies: </strong><br>
                        <div v-for="tech in item.technologies" :key="tech.id" >
                            <i :class="tech.icon" class="fs-1 p-2" :style="{ color: tech.color }"></i>
                            <div class="p-2">{{ tech.name }}</div>
                        </div>
                    </div>
                    <!-- <RouterLink :to="{ name: 'single-project', params: { 'slug': item.slug } }" class="btn btn-success">
                        Read project</RouterLink> -->
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import { store } from '../store';
    export default {
        name: 'CardComponent',
        props: ['item'],
        data() {
            return {
                store
            }
        },
        methods: {
            openModal(project) {
                this.$emit('open-modal', project);
            }
        }
    }
</script>

<style lang="scss" scoped>
@use '../assets/styles/partials/variables' as *;
.card {
    // background-color: $bg-dark;
    cursor: pointer;
    overflow-y: auto;
    height: 300px;
    &::-webkit-scrollbar-thumb {
                        border-radius: 8px;
                        background-color: #363636;
                    }
                &::-webkit-scrollbar-track {
                    border-radius: 8px;
                    background-color: #e7e7e7;
                    border: 1px solid #cacaca;
                    box-shadow: inset 0 0 6px rgba(0, 0, 0, .3);
                }
                &::-webkit-scrollbar {                 
                    width: 12px;
                }
}
</style>