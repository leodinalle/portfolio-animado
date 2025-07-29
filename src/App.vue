<template>
  <div class="app">
    <div class="scroll-content" ref="scrollContent">
      <Background :scrollY="scrollY" />
      <Character :scrollY="scrollY" :isWalking="isWalking" />
      <Speech 
        v-for="(speech, index) in speeches" 
        :key="`speech-${animationKey}-${index}`"
        :speech="speech"
        :isVisible="currentSpeechIndex === index"
        :index="index"
        :scrollY="scrollY"
      />
      
      <div class="scroll-indicator" v-if="scrollY < 100 && !showRestartPrompt">
        <div class="arrow">↓</div>
        <p>Role para baixo para começar a aventura!</p>
        <p class="instruction">Cada mensagem dura 3 segundos de caminhada</p>
      </div>
      
      <!-- Prompt de reinício -->
      <div v-if="showRestartPrompt" class="restart-prompt">
        <div class="restart-card">
          <div class="restart-icon">🎉</div>
          <h2>Fim da apresentação!</h2>
          <p>Você caminhou por {{ Math.round(totalWalkingTime / 1000) }}s</p>
          <p>Deseja reiniciar a animação?</p>
          <button @click="restartAnimation" class="restart-button">
            <span class="button-icon">🔄</span>
            Reiniciar
          </button>
        </div>
      </div>
      
      <div class="scroll-spacer"></div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import Background from './Background.vue'
import Character from './Character.vue'
import Speech from './Speech.vue'

const scrollY = ref(0)
const isWalking = ref(false)
const currentSpeechIndex = ref(-1)
const scrollContent = ref(null)
const showRestartPrompt = ref(false)
const animationKey = ref(0)

// Sistema de timing baseado em tempo de scroll ativo
const speechTimer = ref(null)
const currentMessageTime = ref(0)
const totalWalkingTime = ref(0)
const MESSAGE_DURATION = 3000 // 3 segundos por mensagem
const lastScrollY = ref(0)
const scrollTimeout = ref(null)

const speeches = [
  {
    text: "Oi! Sou Leonardo Dinale",
    icon: "👋"
  },
  {
    text: "Sou apaixonado por tecnologia e inovação",
    icon: "💡"
  },
  {
    text: "Atuo como Desenvolvedor Full Stack",
    icon: "💻"
  },
  {
    text: "Desenvolvo projetos usando Vue.js, React.js e Next.js",
    icon: "🚀"
  },
  {
    text: "Também trabalho com TypeScript, Tailwind CSS e APIs REST",
    icon: "⚙️"
  },
  {
    text: "Adoro criar interfaces bonitas e responsivas",
    icon: "🎨"
  },
  {
    text: "Foco em soluções escaláveis e limpas",
    icon: "🛠️"
  },
  {
    text: "Tecnologias: HTML, CSS, JavaScript, Vue.js, React.js e Next.js",
    icon: "📂"
  },
  {
    text: "Sempre em busca de novos desafios e aprendizado",
    icon: "📚"
  },
  {
    text: "Quer saber mais? Vamos trabalhar juntos!",
    icon: "🤝"
  }
]

const progressPercentage = computed(() => {
  return ((currentSpeechIndex.value + 1) / speeches.length) * 100
})

const timerPercentage = computed(() => {
  return (currentMessageTime.value / MESSAGE_DURATION) * 100
})

const startMessageTimer = () => {
  if (speechTimer.value) {
    clearInterval(speechTimer.value)
  }
  
  speechTimer.value = setInterval(() => {
    // Só conta se está realmente scrollando (isWalking = true)
    if (isWalking.value) {
      currentMessageTime.value += 50
      totalWalkingTime.value += 50
      
      // Verifica se completou 5 segundos da mensagem atual
      if (currentMessageTime.value >= MESSAGE_DURATION) {
        // Avança para próxima mensagem
        if (currentSpeechIndex.value < speeches.length - 1) {
          currentSpeechIndex.value += 1
          currentMessageTime.value = 0 // Reset timer da mensagem
        } else {
          // Terminou todas as mensagens
          clearInterval(speechTimer.value)
          setTimeout(() => {
            showRestartPrompt.value = true
          }, 1000)
        }
      }
    }
    // Se não está andando (isWalking = false), o timer não avança
  }, 50)
}

const detectScrollMovement = () => {
  const currentScroll = scrollY.value
  
  // Detecta se realmente está scrollando (posição mudou)
  if (currentScroll !== lastScrollY.value && currentScroll > 50) {
    isWalking.value = true
    lastScrollY.value = currentScroll
    
    // Inicia primeira mensagem se necessário
    if (currentSpeechIndex.value === -1) {
      currentSpeechIndex.value = 0
      currentMessageTime.value = 0
      totalWalkingTime.value = 0
    }
    
    // Limpa timeout anterior
    if (scrollTimeout.value) {
      clearTimeout(scrollTimeout.value)
    }
    
    // Define timeout para detectar quando parou de scrollar
    scrollTimeout.value = setTimeout(() => {
      isWalking.value = false
    }, 150) // Se não scrollar por 150ms, considera que parou
    
  } else if (currentScroll <= 50) {
    // Voltou ao início
    isWalking.value = false
    if (currentSpeechIndex.value === -1) {
      currentMessageTime.value = 0
    }
  }
}

const handleScroll = () => {
  scrollY.value = window.pageYOffset || document.documentElement.scrollTop
  detectScrollMovement()
}

const restartAnimation = () => {
  // Limpa todos os timers
  if (speechTimer.value) {
    clearInterval(speechTimer.value)
  }
  if (scrollTimeout.value) {
    clearTimeout(scrollTimeout.value)
  }
  
  // Reset completo de todas as variáveis
  showRestartPrompt.value = false
  currentSpeechIndex.value = -1
  currentMessageTime.value = 0
  totalWalkingTime.value = 0
  isWalking.value = false
  lastScrollY.value = 0
  
  // Volta ao topo
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  })
  
  // Reinicia o sistema com delay maior para garantir ordem
  setTimeout(() => {
    // Força reset completo antes de reiniciar
    currentSpeechIndex.value = -1
    currentMessageTime.value = 0
    totalWalkingTime.value = 0
    animationKey.value += 1
    startMessageTimer()
  }, 1500) // Aumentado para 1.5s para garantir reset completo
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
  startMessageTimer()
  handleScroll()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  if (speechTimer.value) {
    clearInterval(speechTimer.value)
  }
  if (scrollTimeout.value) {
    clearTimeout(scrollTimeout.value)
  }
})
</script>

<style scoped>
.app {
  position: relative;
  width: 100vw;
  min-height: 100vh;
  overflow-x: hidden;
}

.scroll-content {
  position: relative;
  width: 100%;
  min-height: 10000vh; /* Aumentado drasticamente para 10 mensagens */
}

.scroll-spacer {
  height: 9950vh; /* Aumentado para comportar todas as 10 mensagens */
  width: 100%;
  pointer-events: none;
}

.scroll-indicator {
  position: fixed;
  bottom: 50px;
  left: 50%;
  transform: translateX(-50%);
  text-align: center;
  color: #2c3e50;
  font-family: 'Comic Sans MS', cursive;
  z-index: 30;
  animation: bounce 2s infinite;
  background: rgba(255, 255, 255, 0.95);
  padding: 20px 25px;
  border-radius: 20px;
  border: 2px solid #2c3e50;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  max-width: 300px;
}

.instruction {
  font-size: 0.9rem;
  color: #666;
  margin-top: 10px;
  font-style: italic;
}

.arrow {
  font-size: 2rem;
  margin-bottom: 10px;
  animation: bounce-arrow 1.5s infinite;
}

/* Prompt de reinício */
.restart-prompt {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.85);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 100;
  animation: fade-in 0.6s ease-in-out;
  backdrop-filter: blur(5px);
}

.restart-card {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 50px 40px;
  border-radius: 25px;
  text-align: center;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
  border: 3px solid rgba(255, 255, 255, 0.2);
  max-width: 450px;
  animation: slide-up 0.8s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.restart-icon {
  font-size: 3rem;
  margin-bottom: 20px;
  animation: bounce-icon 2s infinite;
}

.restart-card h2 {
  font-family: 'Comic Sans MS', cursive;
  margin-bottom: 15px;
  font-size: 2.2rem;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.restart-card p {
  font-family: 'Comic Sans MS', cursive;
  margin-bottom: 20px;
  font-size: 1.2rem;
  opacity: 0.9;
}

.restart-button {
  background: linear-gradient(45deg, #FF6B6B, #4ECDC4);
  color: white;
  border: none;
  padding: 18px 35px;
  border-radius: 50px;
  font-family: 'Comic Sans MS', cursive;
  font-size: 1.2rem;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.2);
  display: flex;
  align-items: center;
  gap: 10px;
  margin: 0 auto;
}

.restart-button:hover {
  transform: translateY(-3px) scale(1.05);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  background: linear-gradient(45deg, #FF5252, #26C6DA);
}

.restart-button:active {
  transform: translateY(-1px) scale(1.02);
}

.button-icon {
  font-size: 1.1rem;
  animation: rotate-icon 2s linear infinite;
}

@keyframes fade-in {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes slide-up {
  from {
    transform: translateY(60px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

@keyframes bounce-icon {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

@keyframes rotate-icon {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateX(-50%) translateY(0);
  }
  40% {
    transform: translateX(-50%) translateY(-10px);
  }
  60% {
    transform: translateX(-50%) translateY(-5px);
  }
}

@keyframes bounce-arrow {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

@media (max-width: 768px) {
  .scroll-indicator {
    bottom: 30px;
    font-size: 0.9rem;
    padding: 15px 20px;
    max-width: 250px;
  }
  
  .instruction {
    font-size: 0.8rem;
  }
  
  .arrow {
    font-size: 1.5rem;
  }
  
  .restart-card {
    margin: 20px;
    padding: 35px 25px;
  }
  
  .restart-card h2 {
    font-size: 1.8rem;
  }
  
  .restart-card p {
    font-size: 1.1rem;
  }
  
  .restart-button {
    padding: 15px 30px;
    font-size: 1.1rem;
  }
  
  .restart-icon {
    font-size: 2.5rem;
  }
}
</style>
