<script setup lang="ts">
type MarkerState = 'active' | 'inactive'

type TrackRow = {
  label: string
  markers: MarkerState[]
}

const props = withDefaults(defineProps<{
  geneLabel?: string
  rowLabels?: string[]
}>(), {
  geneLabel: 'Gene A',
  rowLabels: () => ['Controls', 'Disease A', 'Disease B', 'Disease C'],
})

const exons = [
  { left: '28.5%', width: '7.2%' },
  { left: '44.2%', width: '11.6%' },
  { left: '66.2%', width: '7.6%' },
]

const markerPositions = [7, 10, 12.7, 21, 39, 79.5]

const rows: TrackRow[] = [
  { label: props.rowLabels[0], markers: ['inactive', 'inactive', 'active', 'inactive', 'inactive', 'active'] },
  { label: props.rowLabels[1], markers: ['inactive', 'active', 'active', 'inactive', 'inactive', 'active'] },
  { label: props.rowLabels[2], markers: ['inactive', 'inactive', 'active', 'inactive', 'inactive', 'active'] },
  { label: props.rowLabels[3], markers: ['active', 'active', 'active', 'inactive', 'active', 'inactive'] },
]
</script>

<template>
  <div class="comparison-diagram">
    <div
      v-for="row in rows"
      :key="row.label"
      class="comparison-row"
    >
      <div class="gene-track">
        <div class="gene-line" />
        <div class="gene-segment" />
        <div
          v-for="exon in exons"
          :key="`${row.label}-${exon.left}`"
          class="exon"
          :style="{ left: exon.left, width: exon.width }"
        />
        <div
          v-for="(site, index) in markerPositions"
          :key="`${row.label}-${site}`"
          class="marker"
          :class="row.markers[index]"
          :style="{ left: `${site}%` }"
        />
        <div class="transcription-arrow" />
      </div>
      <div class="row-label">{{ row.label }}</div>
    </div>

    <div class="gene-note">
      <span>{{ geneLabel }}</span>
    </div>
  </div>
</template>

<style scoped>
.comparison-diagram {
  display: grid;
  gap: 0.6rem;
  width: 100%;
}

.comparison-row {
  display: grid;
  grid-template-columns: minmax(0, 1fr) 8.8rem;
  align-items: center;
  column-gap: 1rem;
}

.gene-track {
  position: relative;
  height: 3rem;
}

.gene-line {
  position: absolute;
  top: 1.5rem;
  left: 0.7rem;
  right: 0;
  height: 0.3rem;
  background: #111;
}

.gene-segment {
  position: absolute;
  top: 1.5rem;
  left: 27.5%;
  width: 50.5%;
  height: 0.3rem;
  background: #2a83ab;
}

.exon {
  position: absolute;
  top: 0.78rem;
  height: 1rem;
  background: #237fa7;
  border: 1.5px solid #175978;
  box-sizing: border-box;
}

.marker {
  position: absolute;
  top: 0;
  width: 0.18rem;
  height: 1.55rem;
  background: #395fa0;
}

.marker::before {
  content: "";
  position: absolute;
  top: -0.05rem;
  left: 50%;
  width: 0.86rem;
  height: 0.86rem;
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
  top: 0.2rem;
  left: 24%;
  width: 2.2rem;
  height: 1.15rem;
  border-top: 0.16rem solid #111;
  border-left: 0.16rem solid #111;
}

.transcription-arrow::after {
  content: "";
  position: absolute;
  top: -0.3rem;
  right: -0.08rem;
  border-top: 0.26rem solid transparent;
  border-bottom: 0.26rem solid transparent;
  border-left: 0.58rem solid #111;
}

.row-label {
  color: #ef6200;
  font-size: 1rem;
  font-weight: 500;
  text-align: left;
}

.gene-note {
  width: min(100%, 10rem);
  margin: 0.7rem auto 0;
  border: 3px solid #474747;
  background: #fff;
  padding: 0.35rem 1rem;
  text-align: center;
}

.gene-note span {
  color: #1a9d74;
  font-size: 1.7rem;
  font-style: italic;
  line-height: 1.1;
}
</style>
