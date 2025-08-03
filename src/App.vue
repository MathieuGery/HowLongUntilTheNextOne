<template>
  <div class="countdown-container">
    <!-- Étoiles scintillantes en arrière-plan -->
    <div class="stars">
      <div class="star" v-for="n in 20" :key="n" :style="getStarStyle(n)">✨</div>
    </div>
    
    <!-- Titre simple -->
    <h1 class="countdown-title">
      Le prochain gîte c'est dans...
    </h1>
    
    <!-- Éléments décoratifs qui bougent -->
    <div class="floating-elements">
      <div class="floating-emoji">🚀</div>
      <div class="floating-emoji">⭐</div>
      <div class="floating-emoji">🎊</div>
      <div class="floating-emoji">🎈</div>
    </div>
    
    <div v-if="!isFinished" class="countdown-display">
      <div class="countdown-unit bounce-in" :style="{ animationDelay: '0.1s' }">
        <div class="countdown-number rainbow-text">{{ timeLeft.days }}</div>
        <div class="countdown-label">Jours</div>
      </div>
      <div class="countdown-unit bounce-in" :style="{ animationDelay: '0.2s' }">
        <div class="countdown-number rainbow-text">{{ timeLeft.hours }}</div>
        <div class="countdown-label">Heures</div>
      </div>
      <div class="countdown-unit bounce-in" :style="{ animationDelay: '0.3s' }">
        <div class="countdown-number rainbow-text">{{ timeLeft.minutes }}</div>
        <div class="countdown-label">Minutes</div>
      </div>
      <div class="countdown-unit bounce-in shake" :style="{ animationDelay: '0.4s' }">
        <div class="countdown-number rainbow-text pulse-scale">{{ timeLeft.seconds }}</div>
        <div class="countdown-label">Secondes</div>
      </div>
    </div>
    
    <div v-else class="finished disco-ball">
      <div class="explosion">💥</div>
      🎉 C'est maintenant ! 🎉
      <div class="confetti">
        <div class="confetti-piece" v-for="n in 15" :key="n">🎊</div>
      </div>
    </div>
    
    <div class="target-date">
      📅 Date cible : {{ formattedTargetDate }} 📅
    </div>
    
    <!-- Effet de pluie d'émojis -->
    <div class="emoji-rain">
      <div class="emoji-drop" v-for="n in 10" :key="n" :style="getEmojiStyle(n)">🌟</div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue'

export default {
  name: 'App',
  setup() {
    const timeLeft = ref({
      days: 0,
      hours: 0,
      minutes: 0,
      seconds: 0
    })
    
    const isFinished = ref(false)
    let interval = null
    
    // Récupérer la date cible depuis la variable d'environnement
    const targetDate = new Date(__TARGET_DATE__ || '2025-12-31T23:59:59')
    
    const formattedTargetDate = targetDate.toLocaleDateString('fr-FR', {
      weekday: 'long',
      year: 'numeric',
      month: 'long',
      day: 'numeric',
      hour: '2-digit',
      minute: '2-digit'
    })
    
    const updateCountdown = () => {
      const now = new Date().getTime()
      const target = targetDate.getTime()
      const difference = target - now
      
      if (difference > 0) {
        timeLeft.value = {
          days: Math.floor(difference / (1000 * 60 * 60 * 24)),
          hours: Math.floor((difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)),
          minutes: Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60)),
          seconds: Math.floor((difference % (1000 * 60)) / 1000)
        }
        isFinished.value = false
      } else {
        isFinished.value = true
        if (interval) {
          clearInterval(interval)
        }
      }
    }
    
    onMounted(() => {
      updateCountdown()
      interval = setInterval(updateCountdown, 1000)
    })
    
    onUnmounted(() => {
      if (interval) {
        clearInterval(interval)
      }
    })
    
    return {
      timeLeft,
      isFinished,
      formattedTargetDate,
      getStarStyle: (n) => ({
        top: Math.random() * 100 + '%',
        left: Math.random() * 100 + '%',
        animationDelay: Math.random() * 3 + 's',
        fontSize: (Math.random() * 0.8 + 0.5) + 'rem'
      }),
      getEmojiStyle: (n) => ({
        left: Math.random() * 100 + '%',
        animationDelay: Math.random() * 5 + 's',
        animationDuration: (Math.random() * 3 + 2) + 's'
      })
    }
  }
}
</script>
