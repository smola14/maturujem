<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <div class="container">
    <header>
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </header>

    <RouterView />
  </div>
</template>

<style>
body {
  background-color: #e5e5f7;
  opacity: 0.8;
  background-image: radial-gradient(#444cf7 0.5px, transparent 0.5px),
    radial-gradient(#444cf7 0.5px, #e5e5f7 0.5px);
  background-size: 20px 20px;
  background-position: 0 0, 10px 10px;
}

.container {
  max-width: 1120px;
  padding: 0 3rem;
  margin: 0 auto;
}
</style>
