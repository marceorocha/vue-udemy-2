<script setup>
import ButtonCounter from './components/ButtonCounter.vue';
import { ref, onMounted } from 'vue';
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';


const posts = ref([]);
const postXpage = 10;
const inicio = ref (0);
const fin = ref (postXpage);
const loading = ref(true);

const favorito = ref("");

const cambiarFavorito = (title) => {
  favorito.value = title
} 

const next = () => {
  inicio.value = inicio.value+postXpage;
  fin.value = fin.value+postXpage;
}

const prev = () => {
  inicio.value = inicio.value-postXpage;
  fin.value = fin.value-postXpage;
}

onMounted(async()=> {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value=await res.json()
  } catch (error) {
    console.log(error)
  } finally { 
    setTimeout(()=> {
      loading.value=false
    }, 1500);
   }
})

// fetch('https://jsonplaceholder.typicode.com/posts')
//   .then((res) => res.json())
//   .then((data) => {
//     posts.value=data
//   })
//   .finally(()=> loading.value=false)

</script>

<template>

  <LoadingSpinner v-if="loading" />

<!-- <ButtonCounter></ButtonCounter> -->

<div class="container">

  <h1>Marce</h1>
  <h5>Mi Post Favorito: {{ favorito }}</h5>


<PaginatePost @next="next" @prev="prev" :inicio="inicio" :fin="fin" class="mb-2"/>

<BlogPost 
v-for="post in posts.slice(inicio, fin)"
:key="post.id"
:title="post.title" 
:id="post.id" 
:body="post.body" 
@cambiarFavoritoNombre="cambiarFavorito"
class="mb-2"
/>

</div>
  </template>