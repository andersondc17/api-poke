<script setup>

//import axios from 'axios'
import {useGetData} from '@/composables/getData'

//const pokemons = ref([])

const {data,getData,loading,error} = useGetData()
/*
const getData = async()=>{
    try {
        const {data} = await axios.get('https://pokeapi.co/api/v2/pokemon/')
        pokemons.value = data.results
    } catch (error) {
        console.log(error)
    }
}
*/

getData("https://pokeapi.co/api/v2/pokemon/")

</script>

<template>
    <h1>Pokemones</h1>
    <p v-if="loading">Cargando información...</p>
    <div class="alert alert-danger mt-2" v-if="error">{{error}}</div>
    <div v-if="data">
        <ul class="list-group">
        <li v-for="(poke, index) in data.results" :key="index" class="list-group-item">
            <router-link :to="`/pokemons/${poke.name}`">
                {{poke.name}}
            </router-link>
        </li>
        </ul>
        <div class="mt-2">
            <button :disabled="!data.previous" class="btn btn-success me-2" @click="getData(data.previous)">Previous</button>
            <button :disabled="!data.next" class="btn btn-primary" @click="getData(data.next)">Next</button>
        </div>
    </div>


</template>