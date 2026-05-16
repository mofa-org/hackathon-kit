<script setup lang="ts">
import { useI18n } from '../composables/useI18n'
import { computed } from 'vue'

const { locale } = useI18n()

const isEn = computed(() => locale.value === 'en')
</script>

<template>
  <article class="py-32 bg-bg-primary min-h-screen">
    <div class="max-w-3xl mx-auto px-6 vision-content">

      <!-- Back link -->
      <router-link to="/" class="inline-flex items-center gap-2 text-text-tertiary hover:text-text-primary transition-colors mb-12">
        <svg class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" /></svg>
        {{ isEn ? 'Back to Home' : '返回首页' }}
      </router-link>

      <template v-if="isEn">
        <!-- TODO: Replace with your event's vision content -->
        <h1 class="heading-serif text-4xl md:text-5xl text-text-primary mb-4">[EVENT_NAME] — Vision</h1>
        <p class="text-text-tertiary mb-12">[PARENT_EVENT] | [EVENT_DATES] | [VENUE], [CITY]</p>

        <hr class="border-border mb-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">About This Event</h2>
        <p>Describe your hackathon's vision and mission here. What problems are you trying to solve? What community are you building? What makes your event unique?</p>

        <hr class="border-border my-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">Why This Hackathon</h2>
        <p>Explain the motivation behind your hackathon. What opportunity exists? Why now? Why should builders care?</p>

        <hr class="border-border my-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">What We Explore</h2>
        <p>Describe the themes and areas of exploration for your hackathon.</p>

        <hr class="border-border my-12" />
        <p class="text-center italic text-text-tertiary heading-serif text-lg">Your closing statement here.</p>
      </template>

      <template v-else>
        <!-- TODO: Replace with your event's vision content (Chinese) -->
        <h1 class="heading-serif text-4xl md:text-5xl text-text-primary mb-4">[EVENT_NAME] — 愿景</h1>
        <p class="text-text-tertiary mb-12">[PARENT_EVENT] | [EVENT_DATES] | [VENUE], [CITY]</p>

        <hr class="border-border mb-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">关于此活动</h2>
        <p>在这里描述你的黑客松的愿景和使命。</p>

        <hr class="border-border my-12" />
        <p class="text-center italic text-text-tertiary heading-serif text-lg">结尾寄语。</p>
      </template>

    </div>
  </article>
</template>

<style scoped>
.vision-content p {
  color: var(--color-text-secondary);
  line-height: 1.8;
  margin-bottom: 1rem;
}

.vision-content ul {
  list-style: disc;
  padding-left: 1.5rem;
  margin-bottom: 1rem;
}

.vision-content li {
  color: var(--color-text-secondary);
  line-height: 1.8;
  margin-bottom: 0.5rem;
}

.vision-content a {
  color: var(--color-accent-blue, #3BA7D0);
}
</style>
