<script setup lang="ts">
type GeneState = 'active' | 'inactive'

const props = withDefaults(defineProps<{
  activeLabel?: string
  inactiveLabel?: string
  unmethylatedLabel?: string
  methylatedLabel?: string
  topState?: GeneState
  bottomState?: GeneState
}>(), {
  activeLabel: 'Active gene',
  inactiveLabel: 'Inactive gene',
  unmethylatedLabel: 'Unmethylated cytosine',
  methylatedLabel: 'Methylated cytosine',
  topState: 'active',
  bottomState: 'inactive',
})

const exons = [
  { left: '28.5%', width: '7.2%' },
  { left: '44.2%', width: '11.6%' },
  { left: '66.2%', width: '7.6%' },
]

const topSites = [7, 10, 12.7, 19, 37.6, 84]
const bottomSites = [7, 10, 12.7, 19, 37.6, 84]
</script>

<template>
  <div class="gene-diagram">
    <div class="track-row">
      <div class="gene-track">
        <div class="gene-line" />
        <div class="gene-segment" />
        <div
          v-for="exon in exons"
          :key="`top-${exon.left}`"
          class="exon"
          :style="{ left: exon.left, width: exon.width }"
        />
        <div
          v-for="site in topSites"
          :key="`site-top-${site}`"
          class="marker"
          :class="topState"
          :style="{ left: `${site}%` }"
        />
        <div class="transcription-arrow" />
      </div>
      <div class="state-label">{{ activeLabel }}</div>
    </div>

    <div class="track-row">
      <div class="gene-track">
        <div class="gene-line" />
        <div class="gene-segment" />
        <div
          v-for="exon in exons"
          :key="`bottom-${exon.left}`"
          class="exon"
          :style="{ left: exon.left, width: exon.width }"
        />
        <div
          v-for="site in bottomSites"
          :key="`site-bottom-${site}`"
          class="marker"
          :class="bottomState"
          :style="{ left: `${site}%` }"
        />
        <div class="transcription-arrow" />
      </div>
      <div class="state-label">{{ inactiveLabel }}</div>
    </div>

    <div class="legend-note">
      <div class="legend">
        <div class="legend-item">
          <span class="legend-marker active" />
          <span>{{ unmethylatedLabel }}</span>
        </div>
        <div class="legend-item">
          <span class="legend-marker inactive" />
          <span>{{ methylatedLabel }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.gene-diagram {
  display: grid;
  gap: 1rem;
  width: 100%;
}

.track-row {
  display: grid;
  grid-template-columns: minmax(0, 1fr) 11rem;
  align-items: start;
  column-gap: 1.1rem;
}

.gene-track {
  position: relative;
  height: 6.9rem;
}

.gene-line {
  position: absolute;
  top: 2.65rem;
  left: 1.6rem;
  right: 0.6rem;
  height: 0.36rem;
  background: #121212;
}

.gene-segment {
  position: absolute;
  top: 2.65rem;
  left: 27.5%;
  width: 51.5%;
  height: 0.36rem;
  background: #2a83ab;
}

.exon {
  position: absolute;
  top: 1.55rem;
  height: 1.45rem;
  background: #237fa7;
  border: 2px solid #175978;
  box-sizing: border-box;
}

.marker {
  position: absolute;
  top: 0.55rem;
  width: 0.25rem;
  height: 2.15rem;
  background: #395fa0;
}

.marker::before {
  content: "";
  position: absolute;
  top: -0.05rem;
  left: 50%;
  width: 1rem;
  height: 1rem;
  border-radius: 999px;
  transform: translateX(-50%);
}

.marker.active::before {
  background: #ffffff;
  border: 3px solid #365899;
}

.marker.inactive::before {
  background: #0e4488;
  border: 3px solid #0e4488;
}

.transcription-arrow {
  position: absolute;
  top: 1.2rem;
  left: 23%;
  width: 2rem;
  height: 1.5rem;
  border-top: 0.18rem solid #111;
  border-left: 0.18rem solid #111;
}

.transcription-arrow::after {
  content: "";
  position: absolute;
  top: -0.35rem;
  right: -0.1rem;
  border-top: 0.28rem solid transparent;
  border-bottom: 0.28rem solid transparent;
  border-left: 0.62rem solid #111;
}

.state-label {
  display: grid;
  place-items: center;
  min-height: 1rem;
  border: 3px solid #474747;
  color: #1a9d74;
  font-size: 1.25rem;
  font-weight: 500;
  background: #fff;
  padding: 0.2rem 0.4rem;
  text-align: center;
  margin-top: 1.5rem;
}

.legend-note {
  width: min(100%, 34rem);
  margin: 0.1rem auto 0;
  border: 1px solid #d9e3ea;
  border-radius: 8px;
  background: #f6f7f9;
  box-shadow: 0 8px 20px rgba(15, 76, 129, 0.07);
  padding: 0.7rem 1rem;
}

.legend {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 1rem;
  align-items: center;
}

.legend-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  color: #ef6200;
  font-size: 1rem;
  font-weight: 500;
  line-height: 1.2;
  justify-content: center;
  text-align: left;
}

.legend-marker {
  position: relative;
  width: 1rem;
  height: 1.95rem;
  flex: 0 0 auto;
}

.legend-marker::before {
  content: "";
  position: absolute;
  top: 0;
  left: 50%;
  width: 0.14rem;
  height: 100%;
  background: #365899;
  transform: translateX(-50%);
}

.legend-marker::after {
  content: "";
  position: absolute;
  top: 0;
  left: 50%;
  width: 0.8rem;
  height: 0.8rem;
  border-radius: 999px;
  transform: translateX(-50%);
}

.legend-marker.active::after {
  background: #ffffff;
  border: 3px solid #365899;
}

.legend-marker.inactive::after {
  background: #0e4488;
  border: 3px solid #0e4488;
}
</style>
