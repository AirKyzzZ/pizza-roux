<script setup>
import { ref, onMounted } from 'vue'

const audio = ref(null)
const isPlaying = ref(false)

onMounted(() => {
  if (audio.value) {
    audio.value.play().catch(() => {
      console.log('Autoplay blocked - click play button')
    })
  }
})

const toggleMusic = () => {
  if (audio.value) {
    if (isPlaying.value) {
      audio.value.pause()
    } else {
      audio.value.play()
    }
    isPlaying.value = !isPlaying.value
  }
}
</script>
<template>
  <audio ref="audio" loop>
    <source src="/TarantellaNapoletana.mp3" type="audio/mpeg">
  </audio>
  
  <button @click="toggleMusic" class="music-toggle">
    {{ isPlaying ? 'Pause Music' : 'Play Music' }}
  </button>
</template>
