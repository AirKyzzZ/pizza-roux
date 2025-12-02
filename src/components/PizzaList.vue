<script setup>
import { ref, computed } from 'vue'
import { pizzas } from '../props/Pizzas.vue'

const basket = ref([])

const counter = computed(() => basket.value.reduce((sum, pizza) => sum + pizza.price, 0))

const addToBasket = (pizza) => {
  basket.value.push(pizza)
  
  const soundFile = pizza.id === 1 ? '/Indian.mp3' : '/clown.mp3'
  const audio = new Audio(soundFile)
  audio.play()
}

const clearBasket = () => {
  basket.value = []
}
</script>

<template>
  <div>
    <div>
      <h1>Liste des Pizzas que vous avez commandé Rhoya : </h1>
      <ul>
        <li v-for="element in basket" :key="element.id" >
          <div class="basket-header">
            <h3>{{ element.name }}</h3>
          </div>
        </li>
      </ul>
      <span class="total-price">Prix total du panier : {{ counter.toFixed(2) }}€</span>
    </div>

    <div class="pizza-list">
      <h2>Nos Pizzas ({{ pizzas.length }})</h2>
      <ul>
        <li v-for="pizza in pizzas" :key="pizza.id" class="pizza-item">
          <div class="pizza-header">
            <h3>{{ pizza.name }}</h3>
            <span class="price">{{ pizza.price.toFixed(2) }}€</span>
            <button @click="addToBasket(pizza)">Ajouter au panier</button>
          </div>
        </li>
      </ul>
      <button @click="clearBasket">Vider le PANIEWW</button>
    </div>
  </div>
</template>