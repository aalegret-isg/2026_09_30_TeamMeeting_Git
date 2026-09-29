<script setup>
import { computed, onUnmounted, ref, watch } from 'vue'
import { useNav } from '@slidev/client'

const props = defineProps({
  // Kept for backwards compatibility with the existing slide markup.
  minutes: { type: Number, default: 15 },
  startAfterPage: { type: Number, default: 1 },
})

const shared = globalThis.__retreatCountUpTimer ||= {
  elapsedSeconds: ref(0),
  interval: null,
  startedAt: null,
  activeUsers: 0,
}

const { currentPage, total } = useNav()

function tick() {
  if (!shared.startedAt) return
  shared.elapsedSeconds.value = Math.max(0, Math.floor((Date.now() - shared.startedAt) / 1000))
}

function startTimer() {
  if (!shared.startedAt) {
    shared.startedAt = Date.now() - shared.elapsedSeconds.value * 1000
  }

  if (shared.interval) return

  tick()
  shared.interval = setInterval(tick, 1000)
}

function stopTimer() {
  if (!shared.interval) return
  clearInterval(shared.interval)
  shared.interval = null
}

shared.activeUsers += 1

watch(
  currentPage,
  (page) => {
    if (page <= props.startAfterPage) {
      stopTimer()
      return
    }

    startTimer()
  },
  { immediate: true }
)

onUnmounted(() => {
  shared.activeUsers = Math.max(0, shared.activeUsers - 1)
  if (shared.activeUsers === 0) stopTimer()
})

const formattedTime = computed(() => {
  const minutes = Math.floor(shared.elapsedSeconds.value / 60)
  const seconds = shared.elapsedSeconds.value % 60
  return `${minutes}:${seconds.toString().padStart(2, '0')}`
})
</script>

<template>
  <div class="countdown-widget" aria-label="Elapsed presentation time">
    <div class="countdown-timer">
      <div class="clock-face" aria-hidden="true">
        <span class="clock-hand hour" />
        <span class="clock-hand minute" />
      </div>
      <div class="countdown-value">{{ formattedTime }}</div>
    </div>

    <div class="countdown-slide">
      {{ currentPage }} / {{ total }}
    </div>
  </div>
</template>

<style scoped>
.countdown-widget {
  display: inline-flex;
  align-items: flex-start;
  gap: 0.55rem;
  padding: 0.24rem 0.45rem;
  border: 1px solid #d9e3ea;
  border-radius: 5px;
  background: rgba(255, 255, 255, 0.94);
  box-shadow: 0 8px 18px rgba(15, 76, 129, 0.08);
  color: #08385f;
}

.countdown-timer {
  display: grid;
  justify-items: center;
  gap: 0.12rem;
  min-width: 0.9rem;
}

.clock-face {
  position: relative;
  width: 1.05rem;
  height: 1.05rem;
  border: 2px solid #0f4c81;
  border-radius: 999px;
  background: #f8fbfd;
}

.clock-hand {
  position: absolute;
  left: 50%;
  bottom: 50%;
  width: 0.12rem;
  transform-origin: bottom center;
  border-radius: 999px;
  background: #0f4c81;
}

.clock-hand.hour {
  height: 0.38rem;
  transform: translateX(-50%) rotate(0deg);
}

.clock-hand.minute {
  height: 0.5rem;
  background: #f26b1d;
  transform: translateX(-50%) rotate(55deg);
}

.countdown-value {
  font-family: "Consolas", "Courier New", monospace;
  font-size: 0.72rem;
  font-weight: 700;
  line-height: 1;
}

.countdown-slide {
  align-self: center;
  padding-left: 0.55rem;
  border-left: 1px solid #d9e3ea;
  font-size: 0.72rem;
  font-weight: 700;
  line-height: 1;
}
</style>