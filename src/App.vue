<script setup>
import {ref} from 'vue'

let num = ref(0)

</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark border-bottom border-body">
    <div class="container-fluid">
      <router-link to="/" class="navbar-brand">NBA</router-link>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expended="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <router-link to="/" class="nav-link" aria-current="page">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/about" class="nav-link">About</router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  <div clas="main">
    <router-view></router-view>
  </div>

</template>


<style>
.navbar-brand{
  font-family: 'Mooli-Regular', sans-serif;
}
.nav-link{
  font-family: 'Mooli-Regular', sans-serif;
}

</style>
