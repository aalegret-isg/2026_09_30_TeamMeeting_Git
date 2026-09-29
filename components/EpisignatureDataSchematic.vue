<script setup lang="ts">
type SiteState = 'methylated' | 'unmethylated'

type MiniGene = {
  label: string
  sites: SiteState[]
}

const diseaseGenes: MiniGene[] = [
  { label: 'Gene A', sites: ['methylated', 'unmethylated', 'methylated', 'unmethylated'] },
  { label: 'Gene B', sites: ['unmethylated', 'unmethylated', 'methylated', 'unmethylated'] },
  { label: 'Gene C', sites: ['unmethylated', 'methylated', 'unmethylated', 'unmethylated'] },
]

const controlGenes: MiniGene[] = [
  { label: 'Gene A', sites: ['unmethylated', 'unmethylated', 'unmethylated', 'methylated'] },
  { label: 'Gene B', sites: ['methylated', 'unmethylated', 'unmethylated', 'methylated'] },
  { label: 'Gene C', sites: ['unmethylated', 'unmethylated', 'methylated', 'unmethylated'] },
]

const rows = [
  { probe: 'cg25324105_BC11', values: ['0.2554', '0.3311', '0.1988', '0.2344'], high: [] },
  { probe: 'cg25383568_TC11', values: ['0.9010', '0.7314', '0.9800', '0.1002'], high: [0, 1, 2] },
  { probe: 'cg25455143_BC11', values: ['0.2311', '0.1352', '0.0991', '0.6003'], high: [3] },
  { probe: 'cg25459778_BC11', values: ['0.1121', '0.1300', '0.1231', '0.0980'], high: [] },
]

const sampleNames = ['sample_1', 'sample_2', 'sample_3', 'sample_4']

function markerStyle(index: number) {
  const lefts = [10, 28, 50, 87]

  return {
    left: `${lefts[index]}%`,
  }
}
</script>

<template>
  <div class="epi-data-schematic">
    <!-- CLICK 1: genes + beta explanation appear -->
    <div v-click="1" class="top-row">
      <div class="cohort-panel disease">
        <h3>Disease A</h3>

        <div class="mini-gene-stack">
          <div
            v-for="gene in diseaseGenes"
            :key="`disease-${gene.label}`"
            class="mini-gene"
            :class="{ 'selected-gene': gene.label === 'Gene C' }"
          >
            <div class="mini-track">
              <div class="mini-line" />
              <div class="mini-segment" />
              <div class="mini-exon one" />
              <div class="mini-exon two" />
              <div class="mini-exon three" />

              <div
                v-for="(site, index) in gene.sites"
                :key="`${gene.label}-${index}`"
                class="mini-marker"
                :class="site"
                :style="markerStyle(index)"
              />
            </div>

            <div class="mini-label">
              {{ gene.label }}
            </div>

            <!-- CLICK 2: full-width orange line below Gene C -->
            <div
              v-if="gene.label === 'Gene C'"
              v-click="2"
              class="gene-c-full-line"
            />
          </div>
        </div>
      </div>

      <div class="cohort-panel controls">
        <h3>Controls</h3>

        <div class="mini-gene-stack">
          <div
            v-for="gene in controlGenes"
            :key="`control-${gene.label}`"
            class="mini-gene"
            :class="{ 'selected-gene': gene.label === 'Gene C' }"
          >
            <div class="mini-track">
              <div class="mini-line" />
              <div class="mini-segment" />
              <div class="mini-exon one" />
              <div class="mini-exon two" />
              <div class="mini-exon three" />

              <div
                v-for="(site, index) in gene.sites"
                :key="`${gene.label}-${index}`"
                class="mini-marker"
                :class="site"
                :style="markerStyle(index)"
              />
            </div>

            <div class="mini-label">
              {{ gene.label }}
            </div>

            <!-- CLICK 2: full-width orange line below Gene C -->
            <div
              v-if="gene.label === 'Gene C'"
              v-click="2"
              class="gene-c-full-line"
            />
          </div>
        </div>
      </div>

      <div class="beta-panel">
        <div class="beta-title">Beta value (&beta;)</div>

        <div class="beta-lines">
          <div>&beta; &isin; [0, 1]</div>

          <div>
            &beta; &asymp; 0
            <span class="arrow">→</span>
            <span class="low">Non-methylated</span>
          </div>

          <div>
            &beta; &asymp; 1
            <span class="arrow">→</span>
            <span class="high">Methylated</span>
          </div>
        </div>
      </div>
    </div>

    <!-- CLICK 3: matrix appears -->
    <div v-click="3" class="matrix-panel">
      <table>
        <thead>
          <tr>
            <th class="probe-head">
              <span class="selected-cpgs-badge">Selected CpGs</span>
            </th>

            <th
              v-for="sample in sampleNames"
              :key="sample"
            >
              {{ sample }}
            </th>
          </tr>
        </thead>

        <tbody>
          <tr
            v-for="row in rows"
            :key="row.probe"
          >
            <th>{{ row.probe }}</th>

            <td
              v-for="(value, index) in row.values"
              :key="`${row.probe}-${index}`"
              :class="{ high: row.high.includes(index), low: !row.high.includes(index) }"
            >
              {{ value }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
.epi-data-schematic {
  position: relative;
  display: grid;
  grid-template-columns: 1fr;
  row-gap: 1.15rem;
  width: 100%;
  min-height: 25rem;
  box-sizing: border-box;
}

.top-row {
  display: grid;
  grid-template-columns: minmax(0, 1fr) minmax(0, 1fr) minmax(16rem, 0.9fr);
  column-gap: 0.85rem;
  align-items: start;
}

.cohort-panel {
  position: relative;
  padding-top: 0.1rem;
}

.cohort-panel h3 {
  margin: 0 0 0.22rem;
  color: #f26b1d;
  font-size: 1.18rem;
  font-weight: 650;
  text-align: center;
}

.cohort-panel h3::after {
  content: "";
  display: block;
  width: 100%;
  height: 0.16rem;
  margin-top: 0.18rem;
  background: #0f4c81;
}

.mini-gene-stack {
  display: grid;
  gap: 0.08rem;
}

.mini-gene {
  position: relative;
  display: grid;
  grid-template-columns: minmax(0, 1fr) 3rem;
  align-items: center;
  gap: 0.25rem;
}

.mini-track {
  position: relative;
  height: 1.55rem;
}

.mini-line {
  position: absolute;
  top: 0.95rem;
  left: 0;
  right: 0;
  height: 0.16rem;
  background: #111;
}

.mini-segment {
  position: absolute;
  top: 0.95rem;
  left: 38%;
  width: 45%;
  height: 0.16rem;
  background: #247fa6;
}

.mini-exon {
  position: absolute;
  top: 0.62rem;
  height: 0.55rem;
  background: #237fa7;
  border: 1px solid #175978;
}

.mini-exon.one {
  left: 39%;
  width: 7%;
}

.mini-exon.two {
  left: 55%;
  width: 10%;
}

.mini-exon.three {
  left: 76%;
  width: 7%;
}

.mini-marker {
  position: absolute;
  top: 0.15rem;
  width: 0.12rem;
  height: 0.85rem;
  background: #365899;
}

.mini-marker::before {
  content: "";
  position: absolute;
  top: -0.02rem;
  left: 50%;
  width: 0.46rem;
  height: 0.46rem;
  border-radius: 999px;
  transform: translateX(-50%);
}

.mini-marker.unmethylated::before {
  background: #fff;
  border: 2px solid #365899;
}

.mini-marker.methylated::before {
  background: #0e4488;
  border: 2px solid #0e4488;
}

.mini-label {
  border: 1px solid #474747;
  color: #1a9d74;
  font-size: 0.44rem;
  font-style: italic;
  font-weight: 700;
  padding: 0.1rem 0.12rem;
  text-align: center;
}

/* Keep Gene C orange */
.selected-gene .mini-label {
  border-color: #f27a25;
  color: #f26b1d;
  background: #fff9f4;
}

/* CLICK 2 emphasis: orange line across the full Gene C row */
.gene-c-full-line {
  position: absolute;
  left: 0;
  right: 0;
  bottom: -0.13rem;
  height: 0.16rem;
  border-radius: 999px;
  background: #f27a25;
  box-shadow: 0 0 0 0.04rem rgba(242, 122, 37, 0.18);
  pointer-events: none;
  z-index: 8;
}

.beta-panel {
  display: grid;
  gap: 0.48rem;
  align-content: start;
  min-width: 0;
  padding-left: 0.3rem;
}

.beta-title {
  border: 2.5px solid #333;
  color: #1a9d74;
  font-size: 1.05rem;
  font-weight: 500;
  padding: 0.38rem 0.5rem;
  text-align: center;
}

.beta-lines {
  display: grid;
  gap: 0.48rem;
  color: #222;
  font-size: 1.05rem;
  line-height: 1.15;
}

.beta-lines .arrow {
  color: #111;
}

.beta-lines .low {
  color: #1a9d74;
}

.beta-lines .high {
  color: #f26b1d;
}

.matrix-panel {
  width: min(100%, 44rem);
  margin: 1.45rem auto 0;
  position: absolute;
  top: 8.5rem;
  left: 50%;
  transform: translateX(-50%);
}

.matrix-panel table {
  width: 100%;
  border-collapse: collapse;
  background: #fff;
  border: 1.5px solid #222;
}

.matrix-panel th,
.matrix-panel td {
  padding: 0.36rem 0.48rem;
  border-bottom: 1px solid #222;
  font-size: 0.92rem;
  text-align: center;
  white-space: nowrap;
}

.matrix-panel thead th {
  font-size: 0.96rem;
  font-weight: 850;
}

.probe-head {
  position: relative;
  text-align: center;
  box-shadow: inset 0.22rem 0 0 #f27a25;
}

.selected-cpgs-badge {
  display: inline-block;
  padding: 0.16rem 0.58rem;
  border: 2px solid #f27a25;
  border-radius: 999px;
  background: #fff9f4;
  color: #b35a18;
  font-size: 0.66rem;
  font-weight: 800;
  line-height: 1;
  white-space: nowrap;
}

.matrix-panel tbody th {
  width: 14rem;
  text-align: center;
  font-weight: 850;
  box-shadow: inset 0.22rem 0 0 #f27a25;
  padding-left: 0.75rem;
}

.matrix-panel td.low {
  color: #1a9d74;
}

.matrix-panel td.high {
  color: #f26b1d;
}
</style>