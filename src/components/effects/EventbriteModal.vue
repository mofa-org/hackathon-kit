<script setup lang="ts">
import { ref, computed } from 'vue'
import { useAuth } from '../../composables/useAuth'
import { useRoute } from 'vue-router'

const { isLoggedIn } = useAuth()
const route = useRoute()
const isHome = computed(() => route.path === '/')

// TODO: Replace with your external registration URL, or remove this component if not needed
const REGISTRATION_URL = ''
const DISCORD_URL = ''
const dismissed = ref(true) // disabled by default — set to false and fill URLs to enable
</script>

<template>
  <Teleport to="body">
    <Transition enter-active-class="transition duration-300" enter-from-class="opacity-0" leave-active-class="transition duration-150" leave-to-class="opacity-0">
      <div v-if="isHome && isLoggedIn && !dismissed && REGISTRATION_URL" class="fixed inset-0 z-[200] flex items-center justify-center p-4">
        <div class="absolute inset-0 bg-black/85 backdrop-blur-sm" />
        <div class="relative w-full max-w-md bg-bg-primary border border-accent-yellow/50 shadow-2xl p-6">
          <button @click="dismissed = true" class="absolute top-3 right-3 text-text-muted hover:text-text-primary">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg>
          </button>

          <div class="text-center mb-5">
            <div class="inline-block px-3 py-1 bg-accent-red/20 text-red-400 text-[10px] font-bold tracking-widest uppercase rounded mb-3">Required for entry</div>
            <h2 class="text-xl font-bold text-text-primary mb-2">External Registration</h2>
            <p class="text-sm text-text-secondary leading-relaxed">
              Complete your <strong class="text-text-primary">external registration</strong> for venue access on event days.
            </p>
          </div>

          <a :href="REGISTRATION_URL" target="_blank" rel="noopener"
            class="block w-full py-3 bg-btn-bg text-btn-text text-sm font-bold uppercase tracking-widest text-center hover:bg-btn-hover transition-colors">
            Register
          </a>

          <a v-if="DISCORD_URL" :href="DISCORD_URL" target="_blank" rel="noopener"
            class="block w-full mt-2 py-2.5 border border-border text-text-secondary text-sm font-bold uppercase tracking-widest text-center hover:border-text-secondary hover:text-text-primary transition-colors flex items-center justify-center gap-2">
            Join Discord
          </a>

          <button @click="dismissed = true" class="block w-full mt-2 py-2 text-xs text-text-muted hover:text-text-secondary text-center uppercase tracking-widest">
            Close
          </button>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>
