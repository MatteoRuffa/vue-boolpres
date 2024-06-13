<template>
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container-fluid">
        <a class="navbar-brand" href="#">
            <!-- <img src="/docs/5.3/assets/brand/bootstrap-logo.svg" alt="Logo" width="30" height="24" class="d-inline-block align-text-top"> -->
            Portfolio
        </a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" 
      aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item" v-for="(link, index) in menuItems" :key="index">
            <router-link :to="{ name: link.routeName }" class="nav-link" active-class="active">
              {{ link.label }}
            </router-link>
          </li>
          
        </ul>
        <div class="ms-auto">
          <a href="http://localhost:8000" class="nav-link">
            <i class="fa-solid fa-user"></i> <span>Area Riservata</span>
          </a>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
    export default {
        name: 'HeaderComponent',
        data() {
        return {
            menuItems: [
                {
                    label: 'Home',
                    routeName: 'home'
                },
                {
                    label: 'Projects',
                    routeName: 'projects'
                },
                // {
                //     label: 'About',
                //     routeName: 'about-us'
                // },
                {
                    label: 'Contact',
                    routeName: 'contact'
                },
                // {
                //   label: 'Categorie',
                //   routeName: 'categories'
                // }
            ],
            // show: false
        }
    }
    }
</script>

<style lang="scss" scoped>
@use '../assets/styles/partials/variables' as *;


</style>
