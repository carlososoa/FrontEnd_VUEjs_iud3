<script setup>
import axios from 'axios';
import {ref,onMounted} from 'vue';
import { useAuthStore } from '../../stores/auth';
import {  sendRequest } from '../../functions'; 
import { useRoute } from 'vue-router';

const route= useRoute();
const authStore = useAuthStore();
axios.defaults.headers.common['Authorization'] = 'Bearer' + authStore.authToken;
const form = ref({id:'',titulo:''});
const id = ref(route.params.id);
onMounted(() => {getPublicacion()});
const getPublicacion = () =>{
    axios.get('api/publicaciones/' + id.value).then(
        response => (form.value = response.data.data)
    );
}


</script>
<template>
        <div class="row">
        <div class="col-md-4 offset-md-4">
            
        </div>
    </div>
    <div class="row mt-3">
        <div class="col-md-6 offset-md-3">            
            <div class="container">
                <div class="row">
                    <div class="col-md-8">
                        <div  class="card mb-4">
                            <div class="card-body">
                                <h2 class="card-title">Post {{ form.id }} {{ form.titulo }} </h2>
                                <!--img :src="'/publicacion.webp' " alt="nuevoPost" height="400" width="300" contain-->
                                <img src="/publicacion.webp" class="img-fluid" alt="Responsive image">
                                <p class="card-text">{{ form.contenido }}</p>
                            </div>
                                <div class="card-footer text-muted">
                                    Publicado el {{ form.updated_at }}
                                </div>
                                
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
    </div>


</template>