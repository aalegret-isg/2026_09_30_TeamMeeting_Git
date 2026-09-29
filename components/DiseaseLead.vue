<script setup lang="ts">
import { computed } from 'vue'

type IconType =
  | 'synapse'
  | 'dna'
  | 'chromosome'
  | 'methylation'
  | 'glycan'
  | 'lysosome'
  | 'mitochondria'
  | 'neuron'
  | 'protein'
  | 'cell'
  | 'genome'
  | 'molecule'

const props = withDefaults(
  defineProps<{
    disease: string
    gene?: string
    project?: string
    prefix?: string
    icon?: IconType
  }>(),
  {
    gene: '',
    project: 'TriViae (SJD arrays) project.',
    prefix: 'Test',
    icon: 'dna',
  },
)

const iconClass = computed(() => `icon-${props.icon}`)
</script>


<template>
  <div class="lead-strip disease-lead">

    <!-- =====================================================
         ANIMATED SCIENTIFIC ICON
         ===================================================== -->

    <div
      class="disease-icon"
      :class="iconClass"
      aria-hidden="true"
    >

      <!-- 1. SYNAPSE -->
      <svg
        v-if="icon === 'synapse'"
        viewBox="0 0 64 64"
      >
        <path
          class="stroke-main synapse-left"
          d="M8 18 C17 18 19 24 24 27"
        />

        <path
          class="stroke-main synapse-right"
          d="M56 18 C47 18 45 24 40 27"
        />

        <circle class="fill-main vesicle v1" cx="18" cy="20" r="2.4" />
        <circle class="fill-main vesicle v2" cx="22" cy="17" r="2.1" />
        <circle class="fill-main vesicle v3" cx="21" cy="24" r="1.9" />

        <path
          class="stroke-soft"
          d="M27 25 L27 39"
        />

        <path
          class="stroke-soft"
          d="M37 25 L37 39"
        />

        <circle class="signal s1" cx="30" cy="32" r="2" />
        <circle class="signal s2" cx="34" cy="32" r="2" />

        <path
          class="stroke-main"
          d="M24 42 C29 38 35 38 40 42"
        />
      </svg>


      <!-- 2. DNA -->
      <svg
        v-else-if="icon === 'dna'"
        viewBox="0 0 64 64"
      >
        <path
          class="stroke-main dna-strand strand-a"
          d="M18 8 C46 20 46 44 18 56"
        />

        <path
          class="stroke-main dna-strand strand-b"
          d="M46 8 C18 20 18 44 46 56"
        />

        <g class="dna-rungs">
          <path d="M24 14 L40 14" />
          <path d="M20 23 L44 23" />
          <path d="M20 32 L44 32" />
          <path d="M20 41 L44 41" />
          <path d="M24 50 L40 50" />
        </g>
      </svg>


      <!-- 3. CHROMOSOME -->
      <svg
        v-else-if="icon === 'chromosome'"
        viewBox="0 0 64 64"
      >
        <path
          class="stroke-main chromosome-arm arm-a"
          d="M20 9 C28 17 31 25 32 32 C31 39 28 47 20 55"
        />

        <path
          class="stroke-main chromosome-arm arm-b"
          d="M44 9 C36 17 33 25 32 32 C33 39 36 47 44 55"
        />

        <circle class="fill-main centromere" cx="32" cy="32" r="4" />
      </svg>


      <!-- 4. METHYLATION -->
      <svg
        v-else-if="icon === 'methylation'"
        viewBox="0 0 64 64"
      >
        <path
          class="stroke-main"
          d="M10 37 C20 20 44 20 54 37"
        />

        <circle
          v-for="x in [17, 25, 33, 41, 49]"
          :key="x"
          class="cpg-dot"
          :cx="x"
          cy="33"
          r="2.5"
        />

        <g class="methyl-group">
          <circle cx="34" cy="16" r="7" />
          <text x="34" y="19">CH₃</text>
        </g>

        <path
          class="stroke-soft methyl-arrow"
          d="M34 23 L34 29"
        />
      </svg>


      <!-- 5. GLYCAN -->
      <svg
        v-else-if="icon === 'glycan'"
        viewBox="0 0 64 64"
      >
        <g class="glycan">
          <path class="stroke-soft" d="M32 49 L32 36" />
          <path class="stroke-soft" d="M32 36 L20 25" />
          <path class="stroke-soft" d="M32 36 L44 25" />

          <circle class="glycan-node n1" cx="32" cy="50" r="5" />
          <circle class="glycan-node n2" cx="32" cy="35" r="5" />
          <circle class="glycan-node n3" cx="19" cy="23" r="5" />
          <circle class="glycan-node n4" cx="45" cy="23" r="5" />

          <rect
            class="glycan-square"
            x="27"
            y="7"
            width="10"
            height="10"
            rx="1.5"
          />

          <path class="stroke-soft" d="M32 17 L32 30" />
        </g>
      </svg>


      <!-- 6. LYSOSOME -->
      <svg
        v-else-if="icon === 'lysosome'"
        viewBox="0 0 64 64"
      >
        <circle
          class="stroke-main lysosome-shell"
          cx="32"
          cy="32"
          r="20"
        />

        <circle class="lysosome-particle p1" cx="24" cy="26" r="3" />
        <circle class="lysosome-particle p2" cx="39" cy="25" r="2.5" />
        <circle class="lysosome-particle p3" cx="31" cy="39" r="3" />
        <circle class="lysosome-particle p4" cx="43" cy="38" r="2" />
      </svg>


      <!-- 7. MITOCHONDRIA -->
      <svg
        v-else-if="icon === 'mitochondria'"
        viewBox="0 0 64 64"
      >
        <path
          class="stroke-main mito-shell"
          d="
            M11 33
            C11 18 24 10 39 13
            C52 15 58 26 53 39
            C48 52 34 56 21 50
            C14 47 11 41 11 33
            Z
          "
        />

        <path
          class="stroke-soft mito-fold"
          d="
            M18 29
            C23 18 29 42 34 29
            C39 17 44 43 49 29
          "
        />
      </svg>


      <!-- 8. NEURON -->
      <svg
        v-else-if="icon === 'neuron'"
        viewBox="0 0 64 64"
      >
        <circle class="stroke-main neuron-body" cx="27" cy="31" r="9" />

        <path class="stroke-main neuron-axon" d="M36 31 C45 31 50 34 57 38" />

        <path class="stroke-soft dendrite d1" d="M19 25 L9 17" />
        <path class="stroke-soft dendrite d2" d="M18 31 L7 31" />
        <path class="stroke-soft dendrite d3" d="M20 37 L10 46" />

        <circle class="fill-main neuron-nucleus" cx="27" cy="31" r="3" />

        <circle class="signal axon-signal" cx="43" cy="32.5" r="2.2" />
      </svg>


      <!-- 9. PROTEIN -->
      <svg
        v-else-if="icon === 'protein'"
        viewBox="0 0 64 64"
      >
        <path
          class="stroke-main protein-chain"
          d="
            M10 38
            C14 16 25 19 28 31
            C31 43 40 44 42 29
            C44 16 56 21 54 38
          "
        />

        <circle class="protein-node n1" cx="13" cy="34" r="3" />
        <circle class="protein-node n2" cx="27" cy="29" r="3" />
        <circle class="protein-node n3" cx="40" cy="35" r="3" />
        <circle class="protein-node n4" cx="53" cy="32" r="3" />
      </svg>


      <!-- 10. CELL -->
      <svg
        v-else-if="icon === 'cell'"
        viewBox="0 0 64 64"
      >
        <circle class="stroke-main cell-shell" cx="32" cy="32" r="22" />
        <circle class="stroke-soft nucleus-shell" cx="34" cy="31" r="9" />
        <circle class="fill-main nucleus-dot" cx="36" cy="29" r="3" />

        <circle class="cell-particle p1" cx="19" cy="24" r="2" />
        <circle class="cell-particle p2" cx="20" cy="41" r="2.5" />
        <circle class="cell-particle p3" cx="47" cy="40" r="2" />
      </svg>


      <!-- 11. GENOME -->
      <svg
        v-else-if="icon === 'genome'"
        viewBox="0 0 64 64"
      >
        <circle class="stroke-main genome-ring" cx="32" cy="32" r="22" />

        <path
          class="stroke-soft genome-path"
          d="
            M17 31
            C22 19 28 43 33 30
            C38 18 45 42 49 29
          "
        />

        <circle class="fill-main genome-marker m1" cx="22" cy="25" r="2.5" />
        <circle class="fill-main genome-marker m2" cx="42" cy="36" r="2.5" />
      </svg>


      <!-- 12. MOLECULE -->
      <svg
        v-else
        viewBox="0 0 64 64"
      >
        <path class="stroke-soft" d="M19 33 L31 20" />
        <path class="stroke-soft" d="M31 20 L45 28" />
        <path class="stroke-soft" d="M45 28 L42 44" />
        <path class="stroke-soft" d="M42 44 L24 46" />
        <path class="stroke-soft" d="M24 46 L19 33" />

        <circle class="molecule-node n1" cx="19" cy="33" r="5" />
        <circle class="molecule-node n2" cx="31" cy="20" r="5" />
        <circle class="molecule-node n3" cx="45" cy="28" r="5" />
        <circle class="molecule-node n4" cx="42" cy="44" r="5" />
        <circle class="molecule-node n5" cx="24" cy="46" r="5" />
      </svg>

    </div>


    <!-- =====================================================
         HEADER TEXT
         ===================================================== -->

    <div class="disease-text">
      <span>
        {{ prefix }}

        <span class="title-highlight">
          {{ disease }}

          <template v-if="gene">
            (<i>{{ gene }}</i>)
          </template>
        </span>.

        {{ project }}
      </span>
    </div>

  </div>
</template>


<style scoped>
/* =========================================================
   HEADER
   ========================================================= */

.disease-lead {
  display: flex;
  align-items: center;

  width: 100%;

  gap: 0.7rem;
}


.disease-text {
  display: flex;
  align-items: center;

  font-size: 1.5rem;
  line-height: 1.2;
}


/* =========================================================
   ICON CONTAINER
   ========================================================= */

.disease-icon {
  position: relative;

  display: flex;
  align-items: center;
  justify-content: center;

  width: 2.25rem;
  height: 2.25rem;

  flex: 0 0 2.25rem;

  color: #f26b1d;
}


.disease-icon svg {
  width: 100%;
  height: 100%;

  overflow: visible;
}


/* =========================================================
   COMMON SVG STYLES
   ========================================================= */

.stroke-main {
  fill: none;

  stroke: #f26b1d;

  stroke-width: 3;

  stroke-linecap: round;
  stroke-linejoin: round;
}


.stroke-soft {
  fill: none;

  stroke: #0f4c81;

  stroke-width: 2.2;

  stroke-linecap: round;
  stroke-linejoin: round;
}


.fill-main {
  fill: #f26b1d;
}


/* =========================================================
   1. SYNAPSE
   ========================================================= */

.vesicle {
  animation: vesicle-bob 1.8s ease-in-out infinite;
}

.v2 {
  animation-delay: 0.25s;
}

.v3 {
  animation-delay: 0.5s;
}


.signal {
  fill: #f26b1d;

  animation: synapse-signal 1.4s ease-in-out infinite;
}

.s2 {
  animation-delay: 0.3s;
}


@keyframes synapse-signal {
  0%,
  100% {
    opacity: 0.2;
    transform: translateX(-2px);
  }

  50% {
    opacity: 1;
    transform: translateX(2px);
  }
}


@keyframes vesicle-bob {
  0%,
  100% {
    transform: translateY(0);
  }

  50% {
    transform: translateY(2px);
  }
}


/* =========================================================
   2. DNA
   ========================================================= */

.dna-strand {
  stroke-dasharray: 90;
  stroke-dashoffset: 90;

  animation: dna-draw 2.6s ease-in-out infinite;
}


.strand-b {
  animation-delay: 0.18s;
}


.dna-rungs path {
  stroke: #0f4c81;

  stroke-width: 2;

  animation: rung-pulse 1.6s ease-in-out infinite;
}


@keyframes dna-draw {
  0% {
    stroke-dashoffset: 90;
    opacity: 0.4;
  }

  45%,
  75% {
    stroke-dashoffset: 0;
    opacity: 1;
  }

  100% {
    stroke-dashoffset: -90;
    opacity: 0.4;
  }
}


@keyframes rung-pulse {
  0%,
  100% {
    opacity: 0.35;
  }

  50% {
    opacity: 1;
  }
}


/* =========================================================
   3. CHROMOSOME
   ========================================================= */

.chromosome-arm {
  transform-origin: 32px 32px;

  animation: chromosome-breathe 2s ease-in-out infinite;
}


.arm-b {
  animation-delay: 0.12s;
}


.centromere {
  animation: centromere-pulse 1.4s ease-in-out infinite;
}


@keyframes chromosome-breathe {
  0%,
  100% {
    transform: scaleX(1);
  }

  50% {
    transform: scaleX(1.08);
  }
}


@keyframes centromere-pulse {
  0%,
  100% {
    transform: scale(0.85);
    transform-origin: 32px 32px;
  }

  50% {
    transform: scale(1.2);
    transform-origin: 32px 32px;
  }
}


/* =========================================================
   4. METHYLATION
   ========================================================= */

.cpg-dot {
  fill: #0f4c81;

  animation: cpg-pulse 1.7s ease-in-out infinite;
}


.cpg-dot:nth-of-type(2) {
  animation-delay: 0.15s;
}

.cpg-dot:nth-of-type(3) {
  animation-delay: 0.3s;
}

.cpg-dot:nth-of-type(4) {
  animation-delay: 0.45s;
}


.methyl-group circle {
  fill: rgba(242, 107, 29, 0.12);

  stroke: #f26b1d;

  stroke-width: 2;
}


.methyl-group text {
  fill: #f26b1d;

  font-size: 7px;
  font-weight: 800;

  text-anchor: middle;
}


.methyl-group {
  transform-origin: 34px 16px;

  animation: methyl-drop 1.8s ease-in-out infinite;
}


@keyframes methyl-drop {
  0%,
  100% {
    transform: translateY(-2px);
  }

  50% {
    transform: translateY(3px);
  }
}


@keyframes cpg-pulse {
  0%,
  100% {
    opacity: 0.35;
  }

  50% {
    opacity: 1;
  }
}


/* =========================================================
   5. GLYCAN
   ========================================================= */

.glycan-node {
  fill: #f26b1d;

  animation: glycan-pulse 1.8s ease-in-out infinite;
}


.glycan-square {
  fill: #0f4c81;

  animation: glycan-pulse 1.8s ease-in-out infinite 0.3s;
}


.n2 {
  animation-delay: 0.15s;
}

.n3 {
  animation-delay: 0.3s;
}

.n4 {
  animation-delay: 0.45s;
}


@keyframes glycan-pulse {
  0%,
  100% {
    transform: scale(0.9);
  }

  50% {
    transform: scale(1.1);
  }
}


/* =========================================================
   6. LYSOSOME
   ========================================================= */

.lysosome-shell {
  animation: lysosome-breathe 2.2s ease-in-out infinite;

  transform-origin: 32px 32px;
}


.lysosome-particle {
  fill: #f26b1d;

  transform-origin: 32px 32px;

  animation: lysosome-orbit 3s linear infinite;
}


.p2 {
  animation-delay: -0.8s;
}

.p3 {
  animation-delay: -1.5s;
}

.p4 {
  animation-delay: -2.2s;
}


@keyframes lysosome-breathe {
  50% {
    transform: scale(1.06);
  }
}


@keyframes lysosome-orbit {
  to {
    transform: rotate(360deg);
  }
}


/* =========================================================
   7. MITOCHONDRIA
   ========================================================= */

.mito-shell {
  transform-origin: 32px 32px;

  animation: mito-breathe 2s ease-in-out infinite;
}


.mito-fold {
  stroke-dasharray: 60;
  stroke-dashoffset: 60;

  animation: mito-energy 2s linear infinite;
}


@keyframes mito-breathe {
  50% {
    transform: scale(1.04);
  }
}


@keyframes mito-energy {
  to {
    stroke-dashoffset: -60;
  }
}


/* =========================================================
   8. NEURON
   ========================================================= */

.neuron-body {
  transform-origin: 27px 31px;

  animation: neuron-pulse 2s ease-in-out infinite;
}


.axon-signal {
  fill: #f26b1d;

  animation: axon-travel 1.5s ease-in-out infinite;
}


@keyframes axon-travel {
  0% {
    transform: translateX(-5px);
    opacity: 0;
  }

  50% {
    opacity: 1;
  }

  100% {
    transform: translateX(10px);
    opacity: 0;
  }
}


@keyframes neuron-pulse {
  50% {
    transform: scale(1.06);
  }
}


/* =========================================================
   9. PROTEIN
   ========================================================= */

.protein-chain {
  stroke-dasharray: 100;

  animation: protein-flow 2.2s linear infinite;
}


.protein-node {
  fill: #f26b1d;

  animation: protein-node 1.6s ease-in-out infinite;
}


@keyframes protein-flow {
  to {
    stroke-dashoffset: -100;
  }
}


@keyframes protein-node {
  50% {
    opacity: 0.35;
  }
}


/* =========================================================
   10. CELL
   ========================================================= */

.cell-shell {
  transform-origin: 32px 32px;

  animation: cell-breathe 2.5s ease-in-out infinite;
}


.nucleus-dot {
  transform-origin: 36px 29px;

  animation: nucleus-pulse 1.5s ease-in-out infinite;
}


.cell-particle {
  fill: #f26b1d;

  animation: particle-fade 1.8s ease-in-out infinite;
}


@keyframes cell-breathe {
  50% {
    transform: scale(1.04);
  }
}


@keyframes nucleus-pulse {
  50% {
    transform: scale(1.35);
  }
}


@keyframes particle-fade {
  50% {
    opacity: 0.25;
  }
}


/* =========================================================
   11. GENOME
   ========================================================= */

.genome-ring {
  stroke-dasharray: 8 5;

  transform-origin: 32px 32px;

  animation: genome-spin 10s linear infinite;
}


.genome-marker {
  animation: marker-pulse 1.4s ease-in-out infinite;
}


.m2 {
  animation-delay: 0.7s;
}


@keyframes genome-spin {
  to {
    transform: rotate(360deg);
  }
}


@keyframes marker-pulse {
  50% {
    transform: scale(1.4);
  }
}


/* =========================================================
   12. MOLECULE
   ========================================================= */

.molecule-node {
  fill: #f26b1d;

  transform-origin: center;

  animation: molecule-pulse 1.6s ease-in-out infinite;
}


.molecule-node:nth-of-type(2) {
  animation-delay: 0.18s;
}

.molecule-node:nth-of-type(3) {
  animation-delay: 0.36s;
}

.molecule-node:nth-of-type(4) {
  animation-delay: 0.54s;
}

.molecule-node:nth-of-type(5) {
  animation-delay: 0.72s;
}


@keyframes molecule-pulse {
  0%,
  100% {
    opacity: 0.55;
  }

  50% {
    opacity: 1;
  }
}
</style>