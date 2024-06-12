<template>
    <div class="d-flex justify-content-between align-items-center">
        <h1>All Projects</h1>
        <select name="technologies" id="technologies" class="form-select" @change="setParams(1)" v-model="tech">
            <option value="">All technologies</option>
            <option :value="technology.id" v-for="technology in store.technologies" :key="technology.id">{{ technology.name }}</option>
        </select>
    </div>

    <div class="row">
        <div class="col-12 col-lg-6" v-if="projects.length < 1">
            <h3>No designs found for the technology: {{ selectedTechnology }} </h3>
        </div>
        <div class="col-12 col-lg-6" v-for="project in filteredProjects" :key="project.id">
            <CardComponent :item="project" @open-modal="handleOpenModal"/>
            <!-- <ModalDetails :project="modalProject" ref="modalDetails" /> -->
        </div>
       
    </div>
    <nav>
        <ul class="pagination">
            <li class="page-item">
                <a class="page-link" :class="{ 'disabled': currentPage <= 1 }" href="#"
                    @click.prevent="setParams(currentPage - 1)">Previous</a>
            </li>

            <li class="page-item" v-for="page in totalPage" :key="page">
                <a class="page-link" :class="{ 'active': currentPage == page }" href="#"
                    @click.prevent="setParams(page)">{{ page }}</a>
            </li>

            <li class="page-item">
                <a class="page-link" :class="{ 'disabled': currentPage >= totalPage }" href="#"
                    @click.prevent="setParams(currentPage + 1)">Next</a>
            </li>
        </ul>
    </nav>
</template>

<script>
import { store } from '../store';
import axios from 'axios';
import CardComponent from '../components/CardComponent.vue';
import ModalDetails from '../components/ModalDetails.vue';

    export default {
        name: 'ProjectList',
        components: {
            CardComponent,
            ModalDetails
        },
        data() {
            return {
                store,
                projects: [],
                currentPage: 0,
                totalPage: 0,
                tech: '',
                params: null,
                modalProject: null,
            }
        },
        methods: {
            setParams(numpage) {
                this.currentPage = numpage;
                this.params = {
                    page: this.currentPage,
                }
                if (this.tech) {
                    this.params.category = this.tech;
                }
                this.getAllProjects();
            },
            getAllProjects() {
                axios.get(this.store.apiBaseUrl + '/projects', { params: this.params }).then((res) => {
                    // console.log(res.data);
                    this.projects = res.data.results.data;
                     console.log(this.projects);
                    //se paginazione
                    this.currentPage = res.data.results.current_page;
                    this.totalPage = res.data.results.last_page;
                    this.params = null;
                }).catch(error => {
                    console.error('Si è verificato un errore:', error);
                });
            },
            handleOpenModal(project) {
                this.modalProject = project;
                this.$refs.modalDetails.open();
            }
        },
        computed: {
            filteredProjects() {
                if (!this.tech) {
                    return this.projects;
                }
                return this.projects.filter(project => project.technologies.some(tech => tech.id === this.tech));
            },
            selectedTechnology() {
                const technology = this.store.technologies.find(technology => technology.id == this.tech);
                return technology ? technology.name : '';
            }
        },
        mounted() {
            this.getAllProjects();
        }
    }
</script>

<style lang="scss" scoped>
    .form-select {
    width: auto;
    }
</style>