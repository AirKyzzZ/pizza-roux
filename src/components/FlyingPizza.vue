<script setup>
import { ref, onMounted } from 'vue'

const pizza = ref(null)
const position = ref({ x: 0, y: 0 })
const velocity = ref({ x: 2, y: 2 })

const movePizza = () => {
  if (!pizza.value) return
  

  position.value.x += velocity.value.x
  position.value.y += velocity.value.y
  
 
  const rect = pizza.value.getBoundingClientRect()
  if (position.value.x <= 0 || position.value.x + rect.width >= window.innerWidth) {
    velocity.value.x *= -1
  }
  if (position.value.y <= 0 || position.value.y + rect.height >= window.innerHeight) {
    velocity.value.y *= -1
  }
  

  pizza.value.style.left = position.value.x + 'px'
  pizza.value.style.top = position.value.y + 'px'
  
  requestAnimationFrame(movePizza)
}

onMounted(() => {

  position.value.x = Math.random() * (window.innerWidth - 100)
  position.value.y = Math.random() * (window.innerHeight - 100)
  

  velocity.value.x = (Math.random() - 0.5) * 4
  velocity.value.y = (Math.random() - 0.5) * 4
  
  movePizza()
})
</script>

<template>
  <img 
    ref="pizza" 
    src="/pizza.png" 
    alt="Flying Pizza" 
    class="flying-pizza"
  />
</template>

<style scoped>
.flying-pizza {
  position: fixed;
  width: 100px;
  height: 100px;
  pointer-events: none;
  z-index: 9999; /* oui geoffroy jai vraiment fait ca */
  animation: spin 2s linear infinite;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>
