<script setup>
import axios from 'axios';
import {ref,onMounted} from 'vue';
import { confirmation } from '../../functions';
import { useAuthStore } from '../../stores/auth';
const authStore = useAuthStore();
axios.defaults.headers.common['Authorization'] = 'Bearer' + authStore.authToken;
//onMounted(() => {getPublicaciones()});
const publicaciones = ref([]);
const load = ref(false);

axios.get('/api/publicaciones').then(
    response => {
        const currentPage = response.data.current_page;
        publicaciones.value = response.data.data;
        load.value = true;
    }
).catch(error =>{
    console.log(error);
})




</script>
<template>
    <div class="row">
        <div class="col-md-4 offset-md-4">
            
        </div>
    </div>
    <div class="row mt-3">
        <div class="col-md-6 offset-md-3">
            <div class="card border border-white text-center" v-if ="!load">
                <div class="card-body">
                    <img src="/loading.gif" class = "img-fluid">
                </div>
            </div>
            <div class="container">
                <div class="row">
                    <div class="col-md-8">
                        <div v-for="post in publicaciones" :key="post.id" class="card mb-4">
                            <div class="card-body">
                                <h2 class="card-title">{{ post.titulo }}</h2>
                                <!--img :src="'/publicacion.webp' " alt="nuevoPost" height="400" width="300" contain-->
                                <img src="/publicacion.webp" class="img-fluid" alt="Responsive image">
                                <p class="card-text">{{ post.contenido }}</p>
                            </div>
                                <div class="card-footer text-muted">
                                    Publicado el {{ post.updated_at }}
                                </div>
                                <ul class="navbar-nav me-auto mb-2 mb-lg-0" v-if="authStore.user">
                                    <li class="nav-item px-lg-5">
                                        <router-link :to="{path:'publicacion/'+ post.id}" 
                                        class = "btn btn-success">  Ver Mas                                      
                                        </router-link>
                                    </li>
                                </ul>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
    </div>
</template>