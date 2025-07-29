<template>
  <div class="character-container" :style="characterStyle">
    <div class="character" :class="{ walking: isWalking }">
      <!-- Cabeça -->
      <div class="head">
        <div class="hair"></div>
        <div class="face">
          <div class="eye eye-left" :class="{ blinking: isBlinking }"></div>
          <div class="eye eye-right" :class="{ blinking: isBlinking }"></div>
          <div class="glasses">
            <div class="lens lens-left"></div>
            <div class="lens lens-right"></div>
            <div class="bridge"></div>
          </div>
          <div class="mouth"></div>
        </div>
      </div>
      
      <!-- Corpo -->
      <div class="body">
        <div class="shirt"></div>
        <div class="arms">
          <div class="arm arm-left" :class="{ walking: isWalking }">
            <div class="laptop">
              <div class="screen"></div>
              <div class="keyboard"></div>
            </div>
          </div>
          <div class="arm arm-right" :class="{ walking: isWalking }"></div>
        </div>
      </div>
      
      <!-- Pernas -->
      <div class="legs">
        <div class="leg leg-left" :class="{ walking: isWalking }"></div>
        <div class="leg leg-right" :class="{ walking: isWalking }"></div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  scrollY: {
    type: Number,
    default: 0
  },
  isWalking: {
    type: Boolean,
    default: false
  }
})

const isBlinking = ref(false)

// Posição do personagem baseada no scroll
const characterStyle = computed(() => {
  const progress = Math.min(props.scrollY / 2000, 0.7)
  const x = progress * 50
  
  return {
    transform: `translateX(${x}vw)`,
    transition: props.isWalking ? 'none' : 'transform 0.3s ease-out'
  }
})

// Animação de piscar
let blinkInterval

const startBlinking = () => {
  const blink = () => {
    isBlinking.value = true
    setTimeout(() => {
      isBlinking.value = false
    }, 150)
  }
  
  blinkInterval = setInterval(() => {
    if (Math.random() > 0.7) {
      blink()
    }
  }, 2000)
}

onMounted(() => {
  startBlinking()
})

onUnmounted(() => {
  if (blinkInterval) {
    clearInterval(blinkInterval)
  }
})
</script>

<style scoped>
.character-container {
  position: fixed;
  bottom: 20%;
  left: 10%;
  z-index: 10;
  transition: transform 0.3s ease-out;
}

.character {
  position: relative;
  width: 80px;
  height: 120px;
  animation: idle 3s ease-in-out infinite;
  /* Removido background de debug */
}

.character.walking {
  animation: walk 0.8s ease-in-out infinite;
}

/* Cabeça */
.head {
  position: relative;
  width: 40px;
  height: 40px;
  margin: 0 auto;
}

.hair {
  position: absolute;
  top: -5px;
  left: -2px;
  width: 44px;
  height: 25px;
  background: #8B4513;
  border-radius: 50% 50% 40% 40%;
  z-index: 1;
}

.face {
  position: relative;
  width: 40px;
  height: 40px;
  background: #FDBCB4;
  border-radius: 50%;
  border: 2px solid #E6A8A0;
}

.eye {
  position: absolute;
  width: 8px;
  height: 8px;
  background: #000;
  border-radius: 50%;
  top: 15px;
  transition: height 0.1s ease;
}

.eye.blinking {
  height: 2px;
  border-radius: 50% 50% 0 0;
}

.eye-left {
  left: 10px;
}

.eye-right {
  right: 10px;
}

.glasses {
  position: absolute;
  top: 12px;
  left: 5px;
  width: 30px;
  height: 15px;
}

.lens {
  position: absolute;
  width: 12px;
  height: 12px;
  border: 2px solid #2F4F4F;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.3);
}

.lens-left {
  left: 0;
}

.lens-right {
  right: 0;
}

.bridge {
  position: absolute;
  top: 6px;
  left: 12px;
  width: 6px;
  height: 2px;
  background: #2F4F4F;
}

.mouth {
  position: absolute;
  bottom: 8px;
  left: 50%;
  transform: translateX(-50%);
  width: 8px;
  height: 4px;
  background: #FF69B4;
  border-radius: 0 0 50% 50%;
}

/* Corpo */
.body {
  position: relative;
  width: 50px;
  height: 40px;
  margin: 5px auto 0;
}

.shirt {
  width: 50px;
  height: 40px;
  background: #000;
  border-radius: 10px 10px 5px 5px;
  border: 2px solid #333;
}

.arms {
  position: absolute;
  top: 5px;
  width: 100%;
  height: 30px;
}

.arm {
  position: absolute;
  width: 15px;
  height: 30px;
  background: #FDBCB4;
  border: 2px solid #E6A8A0;
  border-radius: 10px;
}

.arm-left {
  left: -10px;
  transform-origin: top center;
}

.arm-right {
  right: -10px;
  transform-origin: top center;
}

.laptop {
  position: absolute;
  bottom: -15px;
  left: -8px;
  width: 20px;
  height: 15px;
  background: #2F4F4F;
  border-radius: 2px;
  transform: rotate(-10deg);
}

.screen {
  width: 18px;
  height: 12px;
  background: #000080;
  border: 1px solid #000;
  border-radius: 1px;
  margin: 1px;
}

.keyboard {
  width: 18px;
  height: 2px;
  background: #696969;
  margin: 0 1px;
}

/* Pernas */
.legs {
  position: relative;
  width: 60px;
  height: 35px;
  margin: 0 auto;
}

.leg {
  position: absolute;
  width: 18px;
  height: 35px;
  background: #000080;
  border: 2px solid #000050;
  border-radius: 5px;
  transform-origin: top center;
}

.leg-left {
  left: 10px;
}

.leg-right {
  right: 10px;
}

/* Animações */
@keyframes idle {
  0%, 100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-2px);
  }
}

@keyframes walk {
  0% {
    transform: translateY(0px);
  }
  25% {
    transform: translateY(-3px);
  }
  50% {
    transform: translateY(0px);
  }
  75% {
    transform: translateY(-1px);
  }
  100% {
    transform: translateY(0px);
  }
}

.walking .arm-left {
  animation: arm-swing-left 0.8s ease-in-out infinite;
}

.walking .arm-right {
  animation: arm-swing-right 0.8s ease-in-out infinite;
}

.walking .leg-left {
  animation: leg-walk-left 0.8s ease-in-out infinite;
}

.walking .leg-right {
  animation: leg-walk-right 0.8s ease-in-out infinite;
}

@keyframes arm-swing-left {
  0%, 100% {
    transform: rotate(10deg);
  }
  50% {
    transform: rotate(-5deg);
  }
}

@keyframes arm-swing-right {
  0%, 100% {
    transform: rotate(-10deg);
  }
  50% {
    transform: rotate(5deg);
  }
}

@keyframes leg-walk-left {
  0%, 100% {
    transform: rotate(0deg);
  }
  50% {
    transform: rotate(15deg);
  }
}

@keyframes leg-walk-right {
  0%, 100% {
    transform: rotate(0deg);
  }
  50% {
    transform: rotate(-15deg);
  }
}

@media (max-width: 768px) {
  .character-container {
    left: 5%;
    bottom: 25%;
  }
  
  .character {
    width: 60px;
    height: 90px;
  }
  
  .head {
    width: 30px;
    height: 30px;
  }
  
  .face {
    width: 30px;
    height: 30px;
  }
  
  .body {
    width: 40px;
    height: 30px;
  }
  
  .shirt {
    width: 40px;
    height: 30px;
  }
}
</style>
