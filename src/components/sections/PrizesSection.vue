<script setup lang="ts">
import { useI18n } from '../../composables/useI18n'

const { t } = useI18n()

const gold = '#D4A017'

// TODO: Configure your awards here
const awards = [
  { key: 'award1', color: gold },
  { key: 'award2', color: gold },
  { key: 'award3', color: gold },
]
</script>

<template>
  <section id="awards" class="relative py-32 bg-bg-primary overflow-hidden">
    <div class="max-w-4xl mx-auto px-6">
      <div class="text-center mb-8 reveal">
        <h2 class="text-4xl md:text-5xl">
          <span class="heading-serif accent-text">{{ t('awards.title') }}</span>
        </h2>
      </div>

      <p class="text-center text-text-secondary mb-16 reveal">{{ t('awards.subtitle') }}</p>

      <!-- Awards -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 max-w-4xl mx-auto reveal-scale reveal-delay-1">
        <div v-for="award in awards" :key="award.key" class="flex flex-col items-center text-center">
          <div class="medal mb-4" :style="{ '--medal-color': award.color }">
            <div class="medal-ribbon"></div>
            <div class="medal-circle">
              <span class="text-2xl">🏆</span>
            </div>
          </div>
          <h3 class="heading-serif text-lg text-text-primary mb-1">{{ t(`awards.${award.key}`) }}</h3>
          <p v-if="t(`awards.${award.key}By`)" class="prize-amount animate-pulse-slow font-bold text-sm mt-1" :style="{ color: award.color }">{{ t(`awards.${award.key}By`) }}</p>
        </div>
      </div>

      <p class="text-center text-text-secondary text-sm mt-12 reveal">
        {{ t('awards.allParticipants') }} <span class="text-amber-600 font-semibold">{{ t('awards.apiCredits') }}</span> {{ t('awards.fromSponsors') }}
      </p>
    </div>
  </section>
</template>

<style scoped>
.prize-amount {
  letter-spacing: 0.02em;
  text-shadow: 0 0 12px currentColor;
  animation: prize-breathe 2.5s ease-in-out infinite;
}

@keyframes prize-breathe {
  0%, 100% { opacity: 1; text-shadow: 0 0 8px currentColor; }
  50% { opacity: 0.7; text-shadow: 0 0 20px currentColor, 0 0 40px currentColor; }
}
</style>
