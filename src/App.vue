<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import {Suspense} from 'vue'
</script>

<template>
  <header>
    <h1>Test</h1>

    <nav class="*:text-red-500 flex flex-col">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">About</RouterLink>
      <RouterLink to="/simple">Simple page</RouterLink>
      <RouterLink to="/offres/2">offre 2</RouterLink>

    </nav>
  </header>

  <Suspense>
    <RouterView />
  </Suspense>
</template>
