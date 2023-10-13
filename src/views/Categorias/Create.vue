<script setup>
import axios from 'axios';
import {ref,onMounted, nextTick} from 'vue';
import { useAuthStore } from '../../stores/auth';
import { show_alerta, sendRequest } from '../../functions'; 
const authStore = useAuthStore();
axios.defaults.headers.common['Authorization'] = 'Bearer' + authStore.authToken;
const form = ref({nombre:''});
const nameInput = ref('');
const save = () =>{
    sendRequest('POST', form.value, '/api/categorias','');
    form.value.nombre = '';
    nextTick(() => nameInput.value.focus());

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
                            placeholder="Categoria"  class=" form-control" required ref="nameInput">
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