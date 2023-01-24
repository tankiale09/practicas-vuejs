<script setup>
import { ref , computed } from 'vue';

import BlogPost from "./components/BlogPost.vue";
import PaginationPost from './components/PaginationPost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue'

const url = "https://jsonplaceholder.typicode.com/posts";
const favorito = ref('');
const postXpage = 10;
const inicio = ref(0);
const fin = ref(postXpage);
const loading = ref(true);

const cambiarfavoritos = (title) => {
  favorito.value = title;
}

const posts = ref([]);
fetch(url)
  .then(respuesta => respuesta.json())
  .then(data => posts.value = data)
  .finally(() => {
    setTimeout(() => {loading.value = false},700)
  } );
const next = () => {
  inicio.value = inicio.value + postXpage;
  fin.value = fin.value + postXpage;
}

const before = () => {
  inicio.value = inicio.value - postXpage;
  fin.value = fin.value - postXpage;
}


const max =computed( () => posts.value.length);
</script>

<template>
  <LoadingSpinner v-if="loading"></LoadingSpinner>
  <div class="container" v-else>
    <h1 class="mt-5">APP</h1>
    <h2 v-if="!favorito">Mi post favorito: Sin Favoritos </h2>
    <h2 v-else="favorito">Mi post favorito: {{ favorito }} </h2>
    <PaginationPost @nextpage="next" @previous="before" :inicio="inicio" :fin="fin" :leg="max">
    </PaginationPost>
    <BlogPost v-for="post in posts.slice(inicio, fin)" :key="post.id" :title="post.title" :body="post.body"
      @cambiarfavorito="cambiarfavoritos" :id="post.id"> </BlogPost>
  </div>
</template>

<style scoped>

</style>
