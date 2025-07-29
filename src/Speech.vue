<template>
  <div 
    v-if="shouldShow" 
    class="speech-bubble" 
    :style="speechStyle"
    :class="{ 
      'animate-in': isVisible && shouldShow,
      'animate-out': !isVisible && shouldShow,
      'floating': isVisible && shouldShow
    }"
  >
    <div class="speech-content">
      <div class="speech-icon">{{ speech.icon }}</div>
      <p class="speech-text">{{ displayText }}</p>
    </div>
    <div class="speech-tail"></div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'

const props = defineProps({
  speech: {
    type: Object,
    required: true
  },
  isVisible: {
    type: Boolean,
    default: false
  },
  index: {
    type: Number,
    required: true
  },
  scrollY: {
    type: Number,
    required: true
  }
})

const displayText = ref('')
const isTyping = ref(false)
const shouldShow = ref(false)

const speechStyle = computed(() => {
  const characterProgress = Math.min(props.scrollY / 2000, 0.7)
  const characterBaseX = 10
  const characterMovementX = characterProgress * 50
  const characterCurrentX = characterBaseX + characterMovementX
  
  const bubbleX = characterCurrentX - 7
  const bubbleY = 15
  
  return {
    left: `${bubbleX}vw`,
    top: `${bubbleY}%`,
    transform: 'translateZ(0)',
    willChange: 'left'
  }
})

const typeText = async (text) => {
  displayText.value = ''
  isTyping.value = true
  
  for (let i = 0; i <= text.length; i++) {
    displayText.value = text.slice(0, i)
    await new Promise(resolve => setTimeout(resolve, 40))
  }
  
  isTyping.value = false
}

watch(() => props.isVisible, (newValue) => {
  if (newValue) {
    shouldShow.value = true
    typeText(props.speech.text)
  } else if (shouldShow.value) {
    setTimeout(() => {
      shouldShow.value = false
      displayText.value = ''
    }, 200)
  }
})
</script>

<style scoped>
.speech-bubble {
  position: fixed;
  max-width: 320px;
  min-width: 200px;
  background: #FFFFFF;
  border: 3px solid #2C3E50;
  border-radius: 25px;
  padding: 20px 25px;
  z-index: 20;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15), 0 4px 10px rgba(0, 0, 0, 0.1);
  transform: scale(0);
  opacity: 0;
  transition: left 0.1s linear, top 0.1s linear, transform 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55), opacity 0.3s ease;
  will-change: left, top, transform, opacity;
  transform-origin: center bottom;
}

.speech-bubble.animate-in {
  transform: scale(1);
  opacity: 1;
  animation: bounce-in 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55) forwards;
}

.speech-bubble.animate-out {
  transform: scale(0.9);
  opacity: 0;
  transition: all 0.4s ease-out;
}

.speech-bubble.floating {
  animation: float-gentle 3s ease-in-out infinite;
}

.speech-content {
  position: relative;
  text-align: center;
}

.speech-icon {
  font-size: 1.5rem;
  margin-bottom: 8px;
  display: block;
}

.speech-text {
  margin: 0;
  font-family: 'Comic Sans MS', cursive;
  font-size: 16px;
  font-weight: bold;
  color: #2C3E50;
  line-height: 1.5;
  text-align: center;
}

.speech-tail {
  position: absolute;
  bottom: -15px;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 0;
  border-left: 15px solid transparent;
  border-right: 15px solid transparent;
  border-top: 15px solid #FFFFFF;
  filter: drop-shadow(0 3px 3px rgba(0, 0, 0, 0.1));
}

.speech-tail::before {
  content: '';
  position: absolute;
  bottom: 3px;
  left: -18px;
  width: 0;
  height: 0;
  border-left: 18px solid transparent;
  border-right: 18px solid transparent;
  border-top: 18px solid #2C3E50;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
    opacity: 0;
  }
  60% {
    transform: scale(1.05);
    opacity: 0.9;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}

@keyframes float-gentle {
  0%, 100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-8px);
  }
}

.speech-bubble:nth-child(1) { background: #FFE4E1; border-color: #FF69B4; }
.speech-bubble:nth-child(2) { background: #E0F6FF; border-color: #00BFFF; }
.speech-bubble:nth-child(3) { background: #F0FFF0; border-color: #32CD32; }
.speech-bubble:nth-child(4) { background: #FFF8DC; border-color: #FFD700; }
.speech-bubble:nth-child(5) { background: #F0F8FF; border-color: #4169E1; }
.speech-bubble:nth-child(6) { background: #FDF2E9; border-color: #E67E22; }
.speech-bubble:nth-child(7) { background: #F3E5F5; border-color: #9C27B0; }
.speech-bubble:nth-child(8) { background: #E8F5E8; border-color: #4CAF50; }
.speech-bubble:nth-child(9) { background: #FFF3E0; border-color: #FF9800; }
.speech-bubble:nth-child(10) { background: #E3F2FD; border-color: #2196F3; }

@media (max-width: 768px) {
  .speech-bubble {
    max-width: 250px;
    min-width: 180px;
    padding: 16px 20px;
  }
  
  .speech-text {
    font-size: 14px;
  }
  
  .speech-icon {
    font-size: 1.2rem;
  }
  
  .speech-tail {
    border-left-width: 12px;
    border-right-width: 12px;
    border-top-width: 12px;
  }
  
  .speech-tail::before {
    left: -15px;
    border-left-width: 15px;
    border-right-width: 15px;
    border-top-width: 15px;
  }
}
</style>
