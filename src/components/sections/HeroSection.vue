<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import { useCountdown } from '../../composables/useCountdown'
import { useI18n } from '../../composables/useI18n'

const { t } = useI18n()

// TODO: Replace these dates with your event's start/end times
const { days, hours, minutes, seconds, isLive, isOver } = useCountdown('2026-06-15T09:00:00+02:00', '2026-06-16T20:00:00+02:00')

// Typewriter cycling through lines sequentially
const lines = [
  'Hackathon',
  'For Architects of the Future',
  'For Builders Who Ship',
  'For Minds That Question',
]
const typedLine = ref('')
const showCursor = ref(true)
let lineIdx = 0
let typeTimer: ReturnType<typeof setTimeout> | null = null

onMounted(() => {
  let i = 0
  let isDeleting = false

  const typeLoop = () => {
    const current = lines[lineIdx]
    if (!isDeleting) {
      typedLine.value = current.slice(0, ++i)
      if (i > current.length) {
        isDeleting = true
        typeTimer = setTimeout(typeLoop, 2000)
        return
      }
    } else {
      typedLine.value = current.slice(0, --i)
      if (i === 0) {
        isDeleting = false
        lineIdx = (lineIdx + 1) % lines.length
      }
    }
    typeTimer = setTimeout(typeLoop, isDeleting ? 50 : 80)
  }

  typeLoop()
})

onUnmounted(() => {
  if (typeTimer) clearTimeout(typeTimer)
})

const timeUnits = [
  { key: 'hero.days', value: days },
  { key: 'hero.hours', value: hours },
  { key: 'hero.mins', value: minutes },
  { key: 'hero.secs', value: seconds },
]


// Magnetic button effect
const ctaRef = ref<HTMLElement | null>(null)
const ctaTransform = ref('')
function onCtaMouseMove(e: MouseEvent) {
  if (!ctaRef.value) return
  const rect = ctaRef.value.getBoundingClientRect()
  const x = e.clientX - rect.left - rect.width / 2
  const y = e.clientY - rect.top - rect.height / 2
  ctaTransform.value = `translate(${x * 0.3}px, ${y * 0.3}px)`
}
function onCtaMouseLeave() {
  ctaTransform.value = 'translate(0, 0)'
}

// Scroll indicator fade
const isScrolled = ref(false)
onMounted(() => {
  const onScroll = () => {
    isScrolled.value = window.scrollY > 100
    if (isScrolled.value) {
      document.body.classList.add('scrolled')
    } else {
      document.body.classList.remove('scrolled')
    }
  }
  window.addEventListener('scroll', onScroll, { passive: true })
  onUnmounted(() => window.removeEventListener('scroll', onScroll))
})
</script>

<template>
  <section class="relative min-h-screen flex items-center justify-center overflow-hidden bg-bg-primary">
    <!-- Background video -->
    <div class="absolute inset-0">
      <video
        autoplay loop muted playsinline webkit-playsinline
        preload="auto"
        poster="/photos/hero-bg-poster.jpg"
        class="w-full h-full object-cover opacity-30"
        style="will-change: transform; transform: translateZ(0);"
      ><source src="/photos/hero-bg.mp4" type="video/mp4" /></video>
    </div>

    <!-- Gradient overlay -->
    <div
      class="absolute inset-0 opacity-20 animate-gradient-shift"
      style="background: linear-gradient(-45deg, #dc2626, #991b1b, #1e3a8a, #2563eb, #dc2626); background-size: 400% 400%;"
    ></div>


    <!-- Content -->
    <div class="relative z-10 text-center px-6 max-w-6xl mx-auto pt-14">

      <!-- Eyebrow -->
      <div class="inline-flex items-center gap-3 mb-6">
        <div class="h-px w-12 bg-text-primary/30"></div>
        <span class="text-xs text-text-primary/70 font-light tracking-[0.2em] uppercase">{{ t('hero.eyebrow') }}</span>
        <div class="h-px w-12 bg-text-primary/30"></div>
      </div>

      <!-- Main title -->
      <div class="mb-4">
        <!-- TODO: Replace with your event name -->
        <div class="shimmer-text text-6xl md:text-8xl lg:text-[10rem] pb-2" style="font-family: 'Cormorant Garamond', Georgia, serif; font-weight: 400; line-height: 1.1;">[EVENT]</div>
        <div class="text-text-primary/80 text-[0.65rem] md:text-sm lg:text-base font-light uppercase" style="letter-spacing: 0.45em;"><span class="glitch-hover">Hackathon</span></div>
        <div class="heading-serif text-2xl md:text-4xl lg:text-5xl text-text-primary mt-3">{{ typedLine }}<span v-if="showCursor" class="animate-pulse">|</span></div>

        <!-- CTA -->
        <a
          ref="ctaRef"
          href="#teams"
          @mousemove="onCtaMouseMove"
          @mouseleave="onCtaMouseLeave"
          class="hero-cta inline-block mt-6 px-10 py-3 text-white text-sm font-semibold tracking-widest uppercase"
          :style="{ transform: ctaTransform || undefined }"
        >
          {{ t('nav.applyNow') }}
        </a>
      </div>

      <!-- Sponsor line — TODO: Replace with your sponsors -->
      <div class="mb-4">
        <p class="text-xs md:text-sm text-text-primary/80 font-light tracking-wide">
          Powered by our <span class="glitch-hover">sponsors</span>
        </p>
        <div class="flex items-center justify-center gap-6 md:gap-12 mt-4 max-w-sm md:max-w-none mx-auto bg-white/10 backdrop-blur-sm rounded-xl px-6 py-4 inline-flex">
          <!-- TODO: Add your sponsor logos here -->
          <span class="text-text-primary/40 text-sm">[ Sponsor logos go here ]</span>
        </div>
      </div>

      <!-- Divider line -->
      <div class="flex items-center justify-center gap-6 my-6">
        <div class="h-px flex-1 max-w-24 bg-text-primary/30"></div>
        <span class="text-xs text-text-primary tracking-[0.25em] uppercase">{{ t('hero.location') }}</span>
        <div class="h-px flex-1 max-w-24 bg-text-primary/30"></div>
      </div>

      <!-- LIVE indicator -->
      <div v-if="isLive" class="flex justify-center items-center gap-3 mb-12">
        <span class="relative flex h-3 w-3">
          <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-red-400 opacity-75"></span>
          <span class="relative inline-flex rounded-full h-3 w-3 bg-red-500"></span>
        </span>
        <span class="text-lg font-bold text-red-600 uppercase tracking-widest">LIVE NOW</span>
      </div>

      <!-- Countdown with glass cards -->
      <div v-else-if="!isOver" class="flex justify-center gap-2 md:gap-4 mb-6">
        <div
          v-for="unit in timeUnits"
          :key="unit.key"
          class="flex flex-col items-center min-w-[64px] md:min-w-[80px] px-3 py-4 md:px-5 md:py-5 bg-bg-card/60 backdrop-blur-md border border-bg-card/40 shadow-sm countdown-card countdown-pulse"
        >
          <div class="relative overflow-hidden">
            <span class="text-4xl md:text-6xl font-black font-mono text-text-primary tabular-nums inline-block countdown-flip" :key="unit.value.value">
              {{ String(unit.value.value).padStart(2, '0') }}
            </span>
          </div>
          <span class="text-[10px] text-text-primary/60 mt-1 uppercase tracking-[0.15em]">{{ t(unit.key) }}</span>
        </div>
      </div>

      <!-- Event ended -->
      <div v-else class="mb-6">
        <span class="text-lg text-text-primary/60 uppercase tracking-widest font-semibold">Event Concluded</span>
      </div>


    </div>

    <!-- Scroll indicator -->
    <div class="absolute bottom-8 left-1/2 -translate-x-1/2 animate-bounce-slow">
      <div class="w-px h-12 bg-gradient-to-b from-text-muted to-transparent mx-auto"></div>
    </div>
  </section>
</template>

<style scoped>
.hero-cta {
  background: linear-gradient(135deg, #2c3e6b, #16A085);
  box-shadow: 0 0 0 rgba(59, 130, 246, 0);
  transition: transform 0.2s ease-out, box-shadow 0.4s ease, filter 0.4s ease;
}

.hero-cta:hover {
  transform: scale(1.06);
  box-shadow:
    0 0 20px rgba(59, 130, 246, 0.35),
    0 0 60px rgba(22, 160, 133, 0.2);
  filter: brightness(1.15);
}

.hero-cta:active {
  transform: scale(0.98);
  box-shadow: 0 0 10px rgba(59, 130, 246, 0.2);
}
</style>
