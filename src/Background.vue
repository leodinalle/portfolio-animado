<template>
  <div class="background">
    <!-- Céu com nuvens -->
    <div class="sky">
      <div class="cloud cloud-1" :style="{ transform: `translateX(${cloudOffset1}px)` }"></div>
      <div class="cloud cloud-2" :style="{ transform: `translateX(${cloudOffset2}px)` }"></div>
      <div class="cloud cloud-3" :style="{ transform: `translateX(${cloudOffset3}px)` }"></div>
      <div class="cloud cloud-4" :style="{ transform: `translateX(${cloudOffset1 + 400}px)` }"></div>
      <div class="cloud cloud-5" :style="{ transform: `translateX(${cloudOffset2 + 600}px)` }"></div>
      <div class="cloud cloud-6" :style="{ transform: `translateX(${cloudOffset3 + 800}px)` }"></div>
    </div>
    
    <!-- Camada de fundo - Montanhas (com parallax) -->
    <div class="mountains" :style="{ transform: `translateX(${-scrollY * 0.1}px)` }">
      <div class="mountain mountain-1"></div>
      <div class="mountain mountain-2"></div>
      <div class="mountain mountain-3"></div>
      <div class="mountain mountain-4"></div>
      <div class="mountain mountain-5"></div>
      <div class="mountain mountain-6"></div>
      <div class="mountain mountain-7"></div>
      <div class="mountain mountain-8"></div>
      <div class="mountain mountain-9"></div>
      <div class="mountain mountain-10"></div>
      <div class="mountain mountain-11"></div>
      <div class="mountain mountain-12"></div>
      <div class="mountain mountain-13"></div>
      <div class="mountain mountain-14"></div>
      <div class="mountain mountain-15"></div>
      <div class="mountain mountain-16"></div>
      <div class="mountain mountain-17"></div>
      <div class="mountain mountain-18"></div>
      <div class="mountain mountain-19"></div>
      <div class="mountain mountain-20"></div>
      <div class="mountain mountain-21"></div>
      <div class="mountain mountain-22"></div>
      <div class="mountain mountain-23"></div>
      <div class="mountain mountain-24"></div>
      <div class="mountain mountain-25"></div>
      <div class="mountain mountain-26"></div>
      <div class="mountain mountain-27"></div>
      <div class="mountain mountain-28"></div>
      <div class="mountain mountain-29"></div>
      <div class="mountain mountain-30"></div>
      <div class="mountain mountain-31"></div>
      <div class="mountain mountain-32"></div>
      <div class="mountain mountain-33"></div>
      <div class="mountain mountain-34"></div>
      <div class="mountain mountain-35"></div>
      <div class="mountain mountain-36"></div>
      <div class="mountain mountain-37"></div>
      <div class="mountain mountain-38"></div>
      <div class="mountain mountain-39"></div>
      <div class="mountain mountain-40"></div>
      <div class="mountain mountain-41"></div>
      <div class="mountain mountain-42"></div>
      <div class="mountain mountain-43"></div>
      <div class="mountain mountain-44"></div>
      <div class="mountain mountain-45"></div>
      <div class="mountain mountain-46"></div>
      <div class="mountain mountain-47"></div>
      <div class="mountain mountain-48"></div>
    </div>
    
    <!-- Camada média - Prédios antigos (com parallax) -->
    <div class="buildings" :style="{ transform: `translateX(${-scrollY * 0.3}px)` }">
      <!-- Seção 1: Início da cidade -->
      <div class="building building-1">
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="building building-2">
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="chimney"></div>
      </div>
      <div class="building building-3">
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="street-lamp"></div>
      <div class="sign">CAFÉ</div>
      <div class="tree"></div>
      
      <!-- Seção 2: Área residencial -->
      <div class="building building-4">
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="building building-5">
        <div class="window"></div>
        <div class="door"></div>
        <div class="chimney"></div>
      </div>
      <div class="sign sign-2">TECH</div>
      <div class="street-lamp"></div>
      <div class="bench"></div>
      
      <!-- Seção 3: Centro comercial -->
      <div class="building building-6">
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="building building-7">
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="sign sign-3">CODE</div>
      <div class="fountain"></div>
      
      <!-- Seção 4: Distrito empresarial -->
      <div class="building building-8">
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="street-lamp"></div>
      <div class="sign sign-4">DEV</div>
      <div class="building building-9">
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="building building-10">
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
        <div class="chimney"></div>
      </div>
      <div class="sign sign-5">WEB</div>
      <div class="street-lamp"></div>
      <div class="tree"></div>
      
      <!-- Seção 5: Área moderna -->
      <div class="building building-11">
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="building building-12">
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="sign sign-6">APP</div>
      <div class="bench"></div>
      
      <!-- Seção 6: Zona tecnológica -->
      <div class="building building-13">
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="street-lamp"></div>
      <div class="sign sign-7">JS</div>
      <div class="building building-14">
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="building building-15">
        <div class="window"></div>
        <div class="door"></div>
        <div class="chimney"></div>
      </div>
      <div class="sign sign-8">VUE</div>
      <div class="tree"></div>

      <!-- Seção 7: Expansão urbana -->
      <div class="building building-16">
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="sign sign-9">HTML</div>
      <div class="street-lamp"></div>
      <div class="building building-17">
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="building building-18">
        <div class="window"></div>
        <div class="door"></div>
        <div class="chimney"></div>
      </div>
      <div class="sign sign-10">CSS</div>
      <div class="street-lamp"></div>
      <div class="fountain"></div>

      <!-- Seção 8: Distrito inovação -->
      <div class="building building-19">
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="building building-20">
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="sign sign-11">API</div>
      <div class="bench"></div>
      <div class="building building-21">
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="street-lamp"></div>
      <div class="sign sign-12">GIT</div>
      <div class="tree"></div>

      <!-- Seção 9: Centro de dados -->
      <div class="building building-22">
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="building building-23">
        <div class="window"></div>
        <div class="door"></div>
        <div class="chimney"></div>
      </div>
      <div class="sign sign-13">SQL</div>
      <div class="building building-24">
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="sign sign-14">AWS</div>
      <div class="street-lamp"></div>
      <div class="fountain"></div>

      <!-- Seção 10: Futuro digital -->
      <div class="building building-25">
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="building building-26">
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="sign sign-15">SEO</div>
      <div class="bench"></div>
      <div class="building building-27">
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="street-lamp"></div>
      <div class="sign sign-16">UX</div>
      <div class="tree"></div>

      <!-- Seção 11: Inteligência artificial -->
      <div class="building building-28">
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="building building-29">
        <div class="window"></div>
        <div class="door"></div>
        <div class="chimney"></div>
      </div>
      <div class="sign sign-17">AI</div>
      <div class="building building-30">
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="sign sign-18">ML</div>
      <div class="street-lamp"></div>
      <div class="fountain"></div>

      <!-- Seção 12: Final da jornada -->
      <div class="building building-31">
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="building building-32">
        <div class="window"></div>
        <div class="window"></div>
        <div class="window"></div>
        <div class="door"></div>
      </div>
      <div class="sign sign-19">END</div>
      <div class="tree"></div>
      <div class="bench"></div>
      <div class="street-lamp"></div>
    </div>
    
    <!-- Camada frontal - Rua (com parallax) -->
    <div class="street" :style="{ transform: `translateX(${-scrollY * 0.5}px)` }">
      <div class="street-line"></div>
      
      <!-- Elementos variados na rua -->
      <div class="manhole"></div>
      <div class="trash-can"></div>
      <div class="street-flower"></div>
      <div class="manhole" style="margin-left: 200px;"></div>
      <div class="trash-can trash-can-2"></div>
      <div class="street-sign">→</div>
      <div class="manhole" style="margin-left: 300px;"></div>
      <div class="trash-can trash-can-3"></div>
      <div class="street-flower"></div>
      <div class="manhole" style="margin-left: 250px;"></div>
      <div class="trash-can"></div>
      <div class="street-puddle"></div>
      <div class="manhole" style="margin-left: 200px;"></div>
      <div class="trash-can trash-can-2"></div>
      <div class="street-sign">↗</div>
      <div class="manhole" style="margin-left: 300px;"></div>
      <div class="trash-can trash-can-3"></div>
      <div class="street-flower"></div>
      <div class="manhole" style="margin-left: 250px;"></div>
      <div class="trash-can"></div>
      <div class="street-puddle"></div>
      <div class="manhole" style="margin-left: 200px;"></div>
      <div class="trash-can trash-can-2"></div>
      <div class="street-sign">→</div>
      <div class="manhole" style="margin-left: 300px;"></div>
      <div class="trash-can trash-can-3"></div>
      <div class="street-flower"></div>
      <div class="manhole" style="margin-left: 250px;"></div>
      <div class="trash-can"></div>
      <div class="street-puddle"></div>
      <div class="manhole" style="margin-left: 200px;"></div>
      <div class="trash-can trash-can-2"></div>
      <div class="street-sign">↗</div>
      <div class="manhole" style="margin-left: 300px;"></div>
      <div class="trash-can trash-can-3"></div>
      <div class="street-flower"></div>
      <div class="manhole" style="margin-left: 250px;"></div>
      <div class="trash-can"></div>
      <div class="street-puddle"></div>
      <div class="manhole" style="margin-left: 200px;"></div>
      <div class="trash-can trash-can-2"></div>
      <div class="street-sign">→</div>
      <div class="manhole" style="margin-left: 300px;"></div>
      <div class="trash-can trash-can-3"></div>
      <div class="street-flower"></div>
      <div class="manhole" style="margin-left: 250px;"></div>
      <div class="trash-can"></div>
      <div class="street-puddle"></div>
      <div class="manhole" style="margin-left: 200px;"></div>
      <div class="trash-can trash-can-2"></div>
      <div class="street-sign">↗</div>
      <div class="manhole" style="margin-left: 300px;"></div>
      <div class="trash-can trash-can-3"></div>
      <div class="street-flower"></div>
      <div class="manhole" style="margin-left: 250px;"></div>
      <div class="trash-can"></div>
      <div class="street-puddle"></div>
      <div class="manhole" style="margin-left: 200px;"></div>
      <div class="trash-can trash-can-2"></div>
      <div class="street-sign">→</div>
      <div class="manhole" style="margin-left: 300px;"></div>
      <div class="trash-can trash-can-3"></div>
      <div class="street-flower"></div>
      <div class="manhole" style="margin-left: 250px;"></div>
      <div class="trash-can"></div>
      <div class="street-puddle"></div>
      <div class="manhole" style="margin-left: 200px;"></div>
      <div class="trash-can trash-can-2"></div>
      <div class="street-sign">↗</div>
      <div class="manhole" style="margin-left: 300px;"></div>
      <div class="trash-can trash-can-3"></div>
      <div class="street-flower"></div>
      <div class="manhole" style="margin-left: 250px;"></div>
      <div class="trash-can"></div>
      <div class="street-puddle"></div>
      <div class="manhole" style="margin-left: 200px;"></div>
      <div class="trash-can trash-can-2"></div>
      <div class="street-sign">🏁</div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  scrollY: {
    type: Number,
    default: 0
  }
})

const time = ref(0)

// Animação das nuvens
const cloudOffset1 = computed(() => (time.value * 0.5) % (typeof window !== 'undefined' ? window.innerWidth + 200 : 1200) - 100)
const cloudOffset2 = computed(() => (time.value * 0.3 + 300) % (typeof window !== 'undefined' ? window.innerWidth + 200 : 1200) - 100)
const cloudOffset3 = computed(() => (time.value * 0.7 + 600) % (typeof window !== 'undefined' ? window.innerWidth + 200 : 1200) - 100)

let animationFrame

const animate = () => {
  time.value += 1
  animationFrame = requestAnimationFrame(animate)
}

onMounted(() => {
  animate()
})

onUnmounted(() => {
  if (animationFrame) {
    cancelAnimationFrame(animationFrame)
  }
})
</script>

<style scoped>
.background {
  position: fixed;
  top: 0;
  left: 0;
  width: 5000vw; /* Aumentado drasticamente para 10 mensagens */
  height: 100vh;
  pointer-events: none;
  z-index: 1;
}

.sky {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 60%;
  background: linear-gradient(to bottom, #87CEEB 0%, #98D8E8 100%);
  overflow: hidden;
}

.cloud {
  position: absolute;
  background: white;
  border-radius: 50px;
  opacity: 0.8;
}

.cloud::before,
.cloud::after {
  content: '';
  position: absolute;
  background: white;
  border-radius: 50px;
}

.cloud-1, .cloud-4 {
  width: 80px;
  height: 40px;
  top: 20%;
  animation: float 6s ease-in-out infinite;
}

.cloud-1::before, .cloud-4::before {
  width: 50px;
  height: 50px;
  top: -25px;
  left: 10px;
}

.cloud-1::after, .cloud-4::after {
  width: 60px;
  height: 40px;
  top: -15px;
  right: 10px;
}

.cloud-2, .cloud-5 {
  width: 60px;
  height: 30px;
  top: 10%;
  animation: float 8s ease-in-out infinite reverse;
}

.cloud-2::before, .cloud-5::before {
  width: 40px;
  height: 40px;
  top: -20px;
  left: 5px;
}

.cloud-3, .cloud-6 {
  width: 100px;
  height: 50px;
  top: 30%;
  animation: float 10s ease-in-out infinite;
}

.cloud-3::before, .cloud-6::before {
  width: 60px;
  height: 60px;
  top: -30px;
  left: 15px;
}

.cloud-3::after, .cloud-6::after {
  width: 70px;
  height: 50px;
  top: -20px;
  right: 15px;
}

.mountains {
  position: absolute;
  bottom: 40%;
  left: 0;
  width: 3000%; /* Triplicado para mais montanhas */
  height: 30%;
  display: flex;
  align-items: flex-end;
  gap: 30px;
}

.mountain {
  position: relative;
  background: #8B7355;
  clip-path: polygon(0% 100%, 50% 0%, 100% 100%);
}

.mountain-1, .mountain-7, .mountain-13, .mountain-19, .mountain-25, .mountain-31, .mountain-37, .mountain-43 {
  width: 200px;
  height: 150px;
}

.mountain-2, .mountain-8, .mountain-14, .mountain-20, .mountain-26, .mountain-32, .mountain-38, .mountain-44 {
  width: 250px;
  height: 200px;
  background: #A0522D;
}

.mountain-3, .mountain-9, .mountain-15, .mountain-21, .mountain-27, .mountain-33, .mountain-39, .mountain-45 {
  width: 180px;
  height: 120px;
}

.mountain-4, .mountain-10, .mountain-16, .mountain-22, .mountain-28, .mountain-34, .mountain-40, .mountain-46 {
  width: 220px;
  height: 180px;
  background: #8B7355;
}

.mountain-5, .mountain-11, .mountain-17, .mountain-23, .mountain-29, .mountain-35, .mountain-41, .mountain-47 {
  width: 190px;
  height: 160px;
  background: #A0522D;
}

.mountain-6, .mountain-12, .mountain-18, .mountain-24, .mountain-30, .mountain-36, .mountain-42, .mountain-48 {
  width: 240px;
  height: 190px;
  background: #8B7355;
}

.buildings {
  position: absolute;
  bottom: 20%;
  left: 0;
  width: 4000%; /* Quadruplicado para mais prédios */
  height: 50%;
  display: flex;
  align-items: flex-end;
  gap: 20px;
}

.building {
  position: relative;
  background: #D2691E;
  border: 3px solid #8B4513;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 10px;
}

.building-1, .building-9 {
  width: 120px;
  height: 180px;
  background: #CD853F;
}

.building-2, .building-10 {
  width: 100px;
  height: 220px;
  background: #DEB887;
}

.building-3, .building-11 {
  width: 90px;
  height: 150px;
  background: #F4A460;
}

.building-4, .building-12 {
  width: 110px;
  height: 200px;
  background: #D2B48C;
}

.building-5, .building-13 {
  width: 95px;
  height: 170px;
  background: #BC8F8F;
}

.building-6, .building-14 {
  width: 130px;
  height: 190px;
  background: #DEB887;
}

.building-7, .building-15 {
  width: 105px;
  height: 240px;
  background: #CD853F;
}

.building-8 {
  width: 85px;
  height: 160px;
  background: #F4A460;
}

/* Novos elementos urbanos */
.tree {
  width: 40px;
  height: 80px;
  background: #8B4513;
  position: relative;
  margin: 0 15px;
}

.tree::before {
  content: '';
  position: absolute;
  top: -30px;
  left: -15px;
  width: 70px;
  height: 60px;
  background: #228B22;
  border-radius: 50%;
}

.bench {
  width: 60px;
  height: 40px;
  background: #8B4513;
  border: 2px solid #654321;
  margin: 0 20px;
  position: relative;
}

.bench::before {
  content: '';
  position: absolute;
  top: -15px;
  left: 0;
  width: 100%;
  height: 15px;
  background: #8B4513;
  border: 2px solid #654321;
}

.fountain {
  width: 80px;
  height: 60px;
  background: #4682B4;
  border: 3px solid #2F4F4F;
  border-radius: 50%;
  margin: 0 25px;
  position: relative;
}

.fountain::before {
  content: '💧';
  position: absolute;
  top: -10px;
  left: 50%;
  transform: translateX(-50%);
  font-size: 1.2rem;
  animation: fountain-drop 2s infinite;
}

.window {
  width: 25px;
  height: 25px;
  background: #4169E1;
  border: 2px solid #000080;
  margin: 5px;
  border-radius: 3px;
}

.door {
  width: 30px;
  height: 50px;
  background: #8B4513;
  border: 2px solid #654321;
  margin-top: auto;
  border-radius: 5px 5px 0 0;
}

.chimney {
  position: absolute;
  top: -20px;
  right: 10px;
  width: 15px;
  height: 25px;
  background: #696969;
  border: 2px solid #2F4F4F;
}

.street-lamp {
  width: 15px;
  height: 200px;
  background: #2F4F4F;
  position: relative;
  margin: 0 30px;
}

.street-lamp::before {
  content: '';
  position: absolute;
  top: -20px;
  left: -10px;
  width: 35px;
  height: 25px;
  background: #FFD700;
  border-radius: 50%;
  border: 3px solid #DAA520;
}

.sign {
  background: #FF6347;
  color: white;
  padding: 10px 15px;
  font-family: 'Comic Sans MS', cursive;
  font-weight: bold;
  border: 3px solid #DC143C;
  border-radius: 5px;
  height: fit-content;
  margin-top: 50px;
  transform: rotate(-5deg);
}

.sign-2 {
  background: #32CD32;
  border-color: #228B22;
  transform: rotate(3deg);
}

.sign-3 {
  background: #4169E1;
  border-color: #000080;
  transform: rotate(-3deg);
}

.sign-4 {
  background: #FF69B4;
  border-color: #DC143C;
  transform: rotate(5deg);
}

.sign-5 {
  background: #9370DB;
  border-color: #663399;
  transform: rotate(-4deg);
}

.sign-6 {
  background: #FF8C00;
  border-color: #FF6347;
  transform: rotate(2deg);
}

.sign-7 {
  background: #20B2AA;
  border-color: #008B8B;
  transform: rotate(-2deg);
}

.sign-8 {
  background: #32CD32;
  border-color: #228B22;
  transform: rotate(4deg);
}

.sign-9 {
  background: #800080;
  border-color: #4B0082;
  transform: rotate(-5deg);
}

.sign-10 {
  background: #008080;
  border-color: #006400;
  transform: rotate(3deg);
}

.sign-11 {
  background: #8B4513;
  border-color: #A0522D;
  transform: rotate(-3deg);
}

.sign-12 {
  background: #4682B4;
  border-color: #708090;
  transform: rotate(5deg);
}

.sign-13 {
  background: #D8BFD8;
  border-color: #DDA0DD;
  transform: rotate(-4deg);
}

.sign-14 {
  background: #F08080;
  border-color: #FA8072;
  transform: rotate(2deg);
}

.sign-15 {
  background: #E9967A;
  border-color: #F08080;
  transform: rotate(-2deg);
}

.sign-16 {
  background: #BDB76B;
  border-color: #B8860B;
  transform: rotate(4deg);
}

.sign-17 {
  background: #A9A9A9;
  border-color: #808080;
  transform: rotate(-5deg);
}

.sign-18 {
  background: #8FBC8F;
  border-color: #2E8B57;
  transform: rotate(3deg);
}

.sign-19 {
  background: #FF1493;
  border-color: #DC143C;
  transform: rotate(-3deg);
  font-size: 1.2rem;
}

.street {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 4000%; /* Quadruplicado para rua mais longa */
  height: 20%;
  background: #696969;
  border-top: 5px solid #2F4F4F;
  display: flex;
  align-items: center;
  gap: 100px;
  padding: 0 50px;
}

.street-line {
  position: absolute;
  top: 50%;
  left: 0;
  width: 100%;
  height: 5px;
  background: repeating-linear-gradient(
    to right,
    #FFFF00 0px,
    #FFFF00 30px,
    transparent 30px,
    transparent 60px
  );
}

/* Novos elementos da rua */
.street-flower {
  width: 20px;
  height: 30px;
  background: #32CD32;
  position: relative;
  border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
}

.street-flower::before {
  content: '🌸';
  position: absolute;
  top: -10px;
  left: 50%;
  transform: translateX(-50%);
  font-size: 1rem;
}

.street-sign {
  width: 40px;
  height: 40px;
  background: #FFD700;
  border: 3px solid #DAA520;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  font-weight: bold;
  color: #000;
}

.street-puddle {
  width: 60px;
  height: 20px;
  background: #4682B4;
  border-radius: 50%;
  opacity: 0.7;
  position: relative;
}

.street-puddle::before {
  content: '';
  position: absolute;
  top: 2px;
  left: 10px;
  width: 40px;
  height: 16px;
  background: #87CEEB;
  border-radius: 50%;
  opacity: 0.5;
}

.manhole {
  width: 50px;
  height: 50px;
  background: #2F4F4F;
  border-radius: 50%;
  border: 3px solid #000;
  position: relative;
}

.manhole::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 30px;
  height: 30px;
  border: 2px solid #696969;
  border-radius: 50%;
}

.trash-can {
  width: 40px;
  height: 60px;
  background: #228B22;
  border: 3px solid #006400;
  border-radius: 5px;
  position: relative;
}

.trash-can-2 {
  background: #FF4500;
  border-color: #DC143C;
}

.trash-can-3 {
  background: #4169E1;
  border-color: #000080;
}

.trash-can::before {
  content: '';
  position: absolute;
  top: -10px;
  left: -5px;
  width: 50px;
  height: 15px;
  background: inherit;
  border: 3px solid inherit;
  border-radius: 10px;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-10px);
  }
}

@keyframes fountain-drop {
  0%, 100% {
    transform: translateX(-50%) translateY(0px);
  }
  50% {
    transform: translateX(-50%) translateY(-15px);
  }
}

@media (max-width: 768px) {
  .building {
    width: 80px !important;
    height: 120px !important;
  }
  
  .mountain {
    width: 120px !important;
    height: 80px !important;
  }
  
  .tree {
    width: 30px;
    height: 60px;
  }
  
  .bench {
    width: 45px;
    height: 30px;
  }
  
  .fountain {
    width: 60px;
    height: 45px;
  }
}
</style>
