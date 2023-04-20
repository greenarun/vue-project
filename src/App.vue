<script setup>
import { RouterLink, RouterView } from 'vue-router' 
</script>

<template>
  <header>  
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/create">Create</RouterLink> 
      </nav> 
  </header> 
  <RouterView />
</template>

<style scoped> 

header {
  background-color: #f8f9f9;
  height:50px;  
}
 
nav { 
  font-size: 12px;  
  float: right;
  padding: 15px;

}
nav a{margin:0 10px}
 
</style>
