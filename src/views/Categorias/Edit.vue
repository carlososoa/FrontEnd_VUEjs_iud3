<script setup>
import axios from 'axios';
import {ref,onMounted} from 'vue';
import { useAuthStore } from '../../stores/auth';
import {  sendRequest } from '../../functions'; 
import { useRoute } from 'vue-router';

const route= useRoute();
const authStore = useAuthStore();
axios.defaults.headers.common['Authorization'] = 'Bearer' + authStore.authToken;
const form = ref({id:'',nombre:''});
const id = ref(route.params.id);
onMounted(() => {getCategoria()});
const getCategoria = () =>{
    axios.get('api/categorias/' + id.value).then(
        response => (form.value.nombre = response.data.data.nombre)
    );
}
const save = () =>{
    sendRequest('PUT', form.value, '/api/categorias/'+id.value,'/categorias');

}

</script>
<template>
    <div class="row mt-5">
        <div class="col-md-4 offset-md-4">
            <div class="card border border-success">
                <div class="card-header bg-success border-success "></div>
                <div class="card-body">
                    <form @submit.prevent="save">
                        <div class="input-group mb-3">
                            <span class="input-group-text">
                                <i class="fa-solid fa-building"></i>
                            </span>
                            <input autofocus type="text" v-model ="form.nombre"
                            placeholder="Categoria"  class=" form-control" required >
                        </div>                     
                        <div class="d-grid col-10 mx-auto">
                            <button class="btn btn-dark">
                                <i class="fa-solid fa-save"></i>
                                Guardar
                            </button>
                        </div>
                        
                            

                    </form>
                </div>
            </div>            
        </div>

    </div>


</template>