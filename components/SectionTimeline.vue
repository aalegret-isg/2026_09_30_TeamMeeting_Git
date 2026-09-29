<script setup lang="ts">
import { computed } from 'vue'

type SectionKey =
  | 'intro'
  | 's1'
  | 's2'
  | 's3'
  | 's4'
  | 'new'

const sections: { key: SectionKey; label: string }[] = [
  { key: 'intro', label: 'Intro' },
  { key: 's1', label: 'S1' },
  { key: 's2', label: 'S2' },
  { key: 's3', label: 'S3' },
  { key: 's4', label: 'S4' },
  { key: 'new', label: 'New...' },
]

const sectionAliases: Record<string, SectionKey> = {
  i: 'intro',
  objective: 's1',
  obj: 's2',
  wp1: 's3',
  wp2: 's4',
  wp3: 'new',
}

const props = withDefaults(
  defineProps<{
    current?: string
  }>(),
  {
    current: 'intro',
  },
)

const normalizedCurrent = computed<SectionKey>(() => {
  const current = (props.current ?? 'intro').toLowerCase()

  if (sections.some(section => section.key === current))
    return current as SectionKey

  return sectionAliases[current] ?? 'intro'
})

const currentIndex = computed(() =>
  sections.findIndex(section => section.key === normalizedCurrent.value),
)
</script>


<template>
  <div
    class="section-timeline"
    aria-label="Presentation progress"
    data-version="retreat-2026"
  >
    <div
      v-for="(section, index) in sections"
      :key="section.key"
      class="section-node"
      :class="{
        active: normalizedCurrent === section.key,
        past: currentIndex > index,
      }"
    >
      <span class="section-dot" />

      <span class="section-label">
        {{ section.label }}
      </span>

      <span
        v-if="index < sections.length - 1"
        class="section-link"
      />
    </div>
  </div>
</template>


<style scoped>
/* =========================================================
   ORIGINAL LAYOUT
   Sizes and spacing preserved
   ========================================================= */

.section-timeline {
  display: flex;
  align-items: center;
  gap: 0;

  width: min(100%, 54rem);

  margin: 0 0 0.5rem 1.1rem;
}


.section-node {
  position: relative;

  display: flex;
  align-items: center;

  color: #8aa0b3;

  font-size: 0.68rem;
  font-weight: 850;

  text-transform: uppercase;
  letter-spacing: 0.035em;
}


/* =========================================================
   DOT
   Original dimensions preserved
   ========================================================= */

.section-dot {
  position: relative;

  width: 0.62rem;
  height: 0.62rem;

  flex-shrink: 0;

  border-radius: 999px;

  border: 2px solid #b7c6d2;

  background: #fff;

  box-sizing: border-box;

  z-index: 3;

  transition:
    border-color 250ms ease,
    background-color 250ms ease,
    box-shadow 250ms ease;
}


/* =========================================================
   LABEL
   Original dimensions preserved
   ========================================================= */

.section-label {
  margin-left: 0.28rem;
  margin-right: 0.42rem;

  line-height: 1;

  white-space: nowrap;
}


/* =========================================================
   CONNECTING LINE
   Original dimensions preserved
   ========================================================= */

.section-link {
  position: relative;

  width: 1.85rem;
  height: 2px;

  flex-shrink: 0;

  background: #d5dfe7;

  margin-right: 0.42rem;

  overflow: visible;
}


/* =========================================================
   ACTIVE SECTION
   ========================================================= */

.section-node.active {
  color: #f26b1d;
}


.section-node.active .section-dot {
  border-color: #f26b1d;
  background: #f26b1d;

  /*
   * Original static glow preserved.
   */
  box-shadow:
    0 0 0 4px rgba(242, 107, 29, 0.12);

  /*
   * Pulse occurs when the travelling glow reaches it.
   */
  animation:
    active-dot-pulse 1.8s ease-in-out infinite;
}


/*
 * Keep your original outgoing gradient.
 */
.section-node.active .section-link {
  background:
    linear-gradient(
      90deg,
      #f26b1d 0%,
      #d5dfe7 100%
    );
}


/* =========================================================
   PAST SECTION
   ========================================================= */

.section-node.past {
  color: #0f4c81;
}


.section-node.past .section-dot {
  border-color: #0f4c81;
  background: #0f4c81;
}


.section-node.past .section-link {
  background: #0f4c81;
}


/* =========================================================
   TRAVELLING PULSE
   ========================================================= */

/*
 * Select the section immediately BEFORE the active section.
 *
 * Its link is the horizontal line that conceptually leads
 * into the active node.
 *
 * Example:
 *
 *   Models ───────→ Cases
 *                   ↑ active
 *
 * The animated pulse runs across the Models connector.
 */
.section-node:has(+ .section-node.active) .section-link {
  position: relative;

  background: #0f4c81;

  overflow: visible;
}


/*
 * Glowing particle travelling across the horizontal line.
 */
.section-node:has(+ .section-node.active) .section-link::after {
  content: "";

  position: absolute;

  top: 50%;
  left: 0;

  width: 0.46rem;
  height: 0.46rem;

  border-radius: 999px;

  background: #f26b1d;

  transform:
    translate(-50%, -50%);

  opacity: 0;

  box-shadow:
    0 0 4px rgba(242, 107, 29, 0.7),
    0 0 9px rgba(242, 107, 29, 0.55);

  animation:
    link-pulse-travel 1.8s ease-in-out infinite;

  z-index: 5;
}


/*
 * Add a temporary orange glow to the line itself.
 */
.section-node:has(+ .section-node.active) .section-link::before {
  content: "";

  position: absolute;

  inset: 0;

  border-radius: 999px;

  background:
    linear-gradient(
      90deg,
      #0f4c81 0%,
      #0f4c81 35%,
      #f26b1d 65%,
      #f26b1d 100%
    );

  transform-origin: left center;

  opacity: 0;

  animation:
    link-glow 1.8s ease-in-out infinite;
}


/* =========================================================
   ANIMATION:
   horizontal line → active dot
   ========================================================= */

@keyframes link-pulse-travel {
  /*
   * Rest briefly at the beginning.
   */
  0% {
    left: 0%;
    opacity: 0;
    transform:
      translate(-50%, -50%)
      scale(0.7);
  }

  12% {
    opacity: 1;
  }

  /*
   * Travel along the line.
   */
  60% {
    left: 100%;
    opacity: 1;

    transform:
      translate(-50%, -50%)
      scale(1);
  }

  /*
   * Reach the active node.
   */
  70% {
    left: 100%;
    opacity: 0;

    transform:
      translate(-50%, -50%)
      scale(1.5);
  }

  100% {
    left: 100%;
    opacity: 0;
  }
}


@keyframes link-glow {
  0%,
  10% {
    opacity: 0;
    transform: scaleX(0);
  }

  20% {
    opacity: 0.75;
    transform: scaleX(0.15);
  }

  60% {
    opacity: 0.75;
    transform: scaleX(1);
  }

  72% {
    opacity: 0;
    transform: scaleX(1);
  }

  100% {
    opacity: 0;
    transform: scaleX(1);
  }
}


/*
 * The dot waits until the travelling pulse reaches it,
 * and then expands.
 */
@keyframes active-dot-pulse {
  0%,
  55%,
  100% {
    transform: scale(1);

    box-shadow:
      0 0 0 4px rgba(242, 107, 29, 0.12);
  }

  68% {
    transform: scale(1.32);

    box-shadow:
      0 0 0 7px rgba(242, 107, 29, 0.07),
      0 0 10px rgba(242, 107, 29, 0.55);
  }

  82% {
    transform: scale(1);

    box-shadow:
      0 0 0 4px rgba(242, 107, 29, 0.12);
  }
}
</style>