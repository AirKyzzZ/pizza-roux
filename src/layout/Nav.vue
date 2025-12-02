<script setup>
import { ref, computed } from 'vue'
import GeoffroyJS from '../pages/GeoffroyJS.vue'
import PizzaList from '../components/PizzaList.vue'

const routes = {
  '/': PizzaList,
  '/geoffroyjs': GeoffroyJS
}

const getCurrentPath = () => {
  let hash = window.location.hash.replace(/^#/, '')
  return hash ? (hash.startsWith('/') ? hash : '/' + hash) : '/'
}

const currentPath = ref(getCurrentPath())

window.addEventListener('hashchange', () => {
  currentPath.value = getCurrentPath()
})

const currentView = computed(() => {
  return routes[currentPath.value] || PizzaList
})
</script>

<template>
  <nav class="navigation">
    <a href="#/" :class="{ active: currentPath === '/' }">Home</a>
    <a href="#/geoffroyjs" :class="{ active: currentPath === '/geoffroyjs' }">GeoffroyJS</a>
  </nav>
  <component :is="currentView" />
</template>