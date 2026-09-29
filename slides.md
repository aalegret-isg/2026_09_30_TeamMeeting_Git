---
theme: default
title: Episignatures and Rare Disease Analysis
info: |
  Group retreat presentation on episignatures and rare disease analysis.
class: cover-slide
drawings:
  persist: false
transition: fade-out
mdc: true
css:
  - style.css
aspectRatio: 16/9
---

<div class="cover-content">
  <div class="cover-event">Team Meeting - 30 September 2026</div>

  <h1 class="cover-title">EPIFLARE: Episignatures and epigenetic monitoring in rare diseases</h1>

  <br>

  <div class="cover-meta">
    <div class="cover-author">
      Albert Alegret-García (ISGlobal)
    </div>
    <div class="cover-supervisors">
      <span>Supervised by</span>
      Juan R. González // Alejandro Cáceres (ISGlobal) || Luís A. Pérez-Jurado (UPF-IMIM)<br>
      Mercedes Serrano // Roser Urreizti // Dídac Casas (SJD) || Anna Esteve-Codina (CNAG)
    </div>
  </div>

  <div class="absolute cover-logos" style="width: 220px; bottom: 1rem; left: 1%; z-index: 5;">
    <img src="./Images/BRGE_Logo.png" alt="BRGE logo"/>
  </div>

  <div class="absolute cover-logos" style="width: 220px; bottom: 1rem; left: 90%; z-index: 5;">
    <img src="./Images/ISGlobal_Logo.png" alt="ISGlobal logo"/>
  </div>
</div>

---
layout: default
transition: fade
---

<div class="absolute" style="top: 1rem; left: 50%; transform: translateX(-50%); z-index: 5;">
  <SectionTimeline current="intro" />
</div>

<Countdown class="absolute top-2 right-2 z-0" :minutes="20" />

# Available <span class="title-highlight">SJD/CNAG data</span>

<div class="lead-strip flex items-center gap-3" style="width: 100%">
  <div class="text-2xl text-[#f26b1d]" i-carbon-data-table />
  <span>SJD array data.</span>
</div>


<div style="display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 0.55rem;">
  <table class="mini-table" style="font-size: 0.85rem; text-align: center;">
    <thead>
      <tr><th>Syndrome</th><th>N</th></tr>
    </thead>
    <tbody>
      <tr><td>Control</td><td>38</td></tr>
      <tr><td>DDX3X-NDD</td><td>18</td></tr>
      <tr><td><i>JMNG/CFSS</i></td><td>2/2</td></tr>
      <tr><td>LOWE</td><td>8</td></tr>
      <tr><td>MOWS</td><td>18</td></tr>
    </tbody>
  </table>

  <table class="mini-table" style="font-size: 0.85rem; text-align: center;">
    <thead>
      <tr><th>Syndrome</th><th>N</th></tr>
    </thead>
    <tbody>
      <tr><td>PTHS</td><td>32</td></tr>
      <tr><td>PMM2-CDG</td><td>29</td></tr>
      <tr><td>SMS</td><td>14</td></tr>
      <tr><td>Sotos</td><td>35</td></tr>
      <tr><td>FASD</td><td>18</td></tr>
    </tbody>
  </table>

  <table class="mini-table" style="font-size: 0.85rem; text-align: center;">
    <thead>
      <tr><th>Syndrome</th><th>N</th></tr>
    </thead>
    <tbody>
      <tr><td>PMDS</td><td>13</td></tr>
      <tr><td>RSTS</td><td>10</td></tr>
      <tr><td><i>SATB2</i></td><td>17</td></tr>
      <tr><td><i>USP9X</i></td><td>5+2</td></tr>
      <tr><td>ZTTK</td><td>4</td></tr>
    </tbody>
  </table>

</div>

<br>

<div class="lead-strip flex items-center gap-3 absolute" style="left: 5%; top: 70%; width: 43%; z-index: 5;">
  <div class="text-2xl text-[#f26b1d]" i-carbon-flow-stream />
  <span>SJD LR PacBio data.</span>
</div>

<div class="absolute" style="left: 5%; z-index: 5; width: 43%; top: 80%;">
  <div class="metric-card">
    <div class="metric-label">Sotos, TBRS, <i>PKD1</i>, and undiagnosed overgrowth.</div>
  </div>
</div>



<div class="lead-strip flex items-center gap-3 absolute" style="left: 55%; top: 70%; width: 40%; z-index: 5;">
  <div class="text-2xl text-[#f26b1d]" i-carbon-flow-stream />
  <span>CNAG ONT data.</span>
</div>

<div class="absolute" style="left: 55%; z-index: 5; width: 40%; top: 80%;">
  <div class="metric-card">
    <div class="metric-label">20 Trios undiagnosed patients.</div>
  </div>
</div>


<div class="brand-footer">
  <img src="./Images/BRGE_Logo.png" class="footer-left" alt="BRGE logo" style="max-width: 100px;"/>
  <img src="./Images/ISGlobal_Logo.png" class="footer-right" alt="ISGlobal logo" style="max-width: 100px;"/>
</div>

---
layout: default
transition: fade
---

<div class="absolute" style="top: 1rem; left: 50%; transform: translateX(-50%); z-index: 5;">
  <SectionTimeline current="s1" />
</div>

<Countdown class="absolute top-2 right-2 z-0" :minutes="20" />

# Study 1: <span class="title-highlight">RSTS confirmed case</span>


<!-- Click 1: without real cases -->
<div v-click="[1,2]">
  <div class="absolute lead-strip flex items-center gap-3" style="width: 90%">
    <div class="text-2xl text-[#f26b1d]" i-carbon-model-alt />
    <span>In cases without reference datasets, episignatures are difficult to use...</span>
  </div>
  <img
    src="./Images/PCA_paradigm.png" class="absolute wide-figure"
    style="text-align: center; width: 100%; top: 27%; left: 35%; transform: translateX(-50%);"
  />
  <div class="absolute figure-caption" style="text-align: center; top: 50%; left: 70%; width: 20%; transform: translateX(-50%);">RSTS PCA using IGenCO cohort. What can be deduced from this?</div>
</div>

<!-- Click 2: Using synthetic -->
<div v-click="[2,3]">
  <div class="absolute lead-strip flex items-center gap-3" style="width: 90%">
    <div class="text-2xl text-[#f26b1d]" i-carbon-model-alt />
    <span>With synthetic case profiles, we can test syndromes without real cases.</span>
  </div>
  <img
    src="./Images/SVM_paradigm_RSTS.png" class="absolute wide-figure"
    style="text-align: center; width: 45%; top: 27%; left: 25%; transform: translateX(-50%);"
  />
  <img
    src="./Images/PCA_paradigm_WithSyntheticRSTS.png" class="absolute wide-figure"
    style="text-align: center; width: 45%; top: 27%; left: 75%; transform: translateX(-50%);"
  />
  <div class="absolute figure-caption" style="text-align: center; width: 90%; top: 90%; left: 50%; transform: translateX(-50%);">[LEFT] SVM trained using syntetic cases.<br>[RIGHT] PCA show synthetic methylation profiles and controls from public datasets.</div>
</div>

<!-- Click 3: Article -->
<div v-click="[3,4]">
  <div class="absolute lead-strip flex items-center gap-3" style="width: 90%">
    <div class="text-2xl text-[#f26b1d]" i-carbon-model-alt />
    <span>And using real RSTS cases... (PMID: 41309537).</span>
  </div>
  <img
    src="./Images/RSTS_PublicRef.png" class="absolute wide-figure"
    style="text-align: center; width: 75%; top: 27%; left: 50%; transform: translateX(-50%);"
  />
</div>

<!-- Click 4: HC Real public cases -->
<div v-click="[4,5]">
  <div class="absolute lead-strip flex items-center gap-3" style="width: 90%">
    <div class="text-2xl text-[#f26b1d]" i-carbon-model-alt />
    <span>And using real RSTS cases... (PMID: 41309537).</span>
  </div>
  <img
    src="./Images/HC_RSTS_IGenCO.png" class="absolute wide-figure"
    style="text-align: center; width: 100%; top: 25%; left: 50%; transform: translateX(-50%);"
  />
  <div class="absolute figure-caption" style="text-align: center; width: 90%; top: 93%; left: 50%; transform: translateX(-50%);">Hierarchical clustering using IGenCO cases, SJD reference controls and public RSTS japanese cases.</div>
</div>

<!-- Click 4: PCA and scores -->
<div v-click="[5,6]">
  <div class="absolute lead-strip flex items-center gap-3" style="width: 90%">
    <div class="text-2xl text-[#f26b1d]" i-carbon-model-alt />
    <span>And using real RSTS cases... (PMID: 41309537).</span>
  </div>
  <img
    src="./Images/PCA_RSTS_IGenCO.png" class="absolute wide-figure"
    style="text-align: center; width: 45%; top: 25%; left: 25%; transform: translateX(-50%);"
  />
  <img
    src="./Images/SVMscores_SJDmodel.png" class="absolute wide-figure"
    style="text-align: center; width: 45%; top: 25%; left: 75%; transform: translateX(-50%);"
  />
  <div class="absolute figure-caption" style="text-align: center; width: 85%; top: 91%; left: 50%; transform: translateX(-50%);">[LEFT] PCA SJD reference controls and public RSTS japanese cases. IGenCO cases represented on top using the trained transformation.<br>[RIGHT] SVM trained using SJD controls and RSTS japanese cases. Public controls used for comparison.</div>
</div>


<div v-click="6">

  <img src="./Images/RSTS_StudyTitle.png" class="absolute wide-figure"
    style="text-align: center; width: 80%; top: 25%; left: 50%; transform: translateX(-50%);">

</div>

<div class="brand-footer">
  <img src="./Images/BRGE_Logo.png" class="footer-left" alt="BRGE logo" style="max-width: 100px;"/>
  <img src="./Images/ISGlobal_Logo.png" class="footer-right" alt="ISGlobal logo" style="max-width: 100px;"/>
</div>


---
layout: default
transition: fade
---

<div class="absolute" style="top: 1rem; left: 50%; transform: translateX(-50%); z-index: 5;">
  <SectionTimeline current="s2" />
</div>

<Countdown class="absolute top-2 right-2 z-0" :minutes="20" />
<div v-click-hide="3">

# Study 2: <span class="title-highlight">MOWS epi validation</span>

  <div class="lead-strip flex items-center gap-3" style="width: 100%">
    <div class="text-2xl text-[#f26b1d]" i-carbon-qq-plot />
    <span>MOWS results. TriViae (SJD arrays) project.</span>
  </div> 
</div>

<!-- Click 0: Introduction -->
<div class="two-col" v-click-hide="1">
  <div>
  <div class="relative" style="left: 50%; width:4 0%; transform: translateX(-50%); z-index: 5;">
      <div class="metric-card">
        <div class="metric-label">- Screened: 18 MOWS (3 females, 15 males).<br>- Age: 8.3 &plusmn; 8.3.</div>
      </div>
    </div>
  </div>
  <div>
    <div class="relative" style="left: 50%; width:4 0%; transform: translateX(-50%); z-index: 5;">
      <div class="metric-card">
        <div class="metric-label">Test 1 suspected MOWS (no variant), 3 newborns (1 / 14 days old) and 1 missense carrier (very mild MOWS).</div>
      </div>
    </div>
  </div>
</div>

<div v-click-hide="1">
  <img src="./Images/MOWS_PublicRef.png" class="absolute wide-figure"
    style="text-align: center; width: 50%; top: 52%; left: 50%; transform: translateX(-50%);">
</div>

<!-- Click 1: public episignature -->
<div v-click="[1,2]">
  <img
    src="./Images/MOWS_epi.png" class="absolute wide-figure"
    style="text-align: center; width: 100%; top: 25%; left: 50%; transform: translateX(-50%);"
  />
  <div class="absolute figure-caption" style="text-align: center; width: 90%; top: 93%; left: 50%; transform: translateX(-50%);">Public episignature clustering using SJD controls and MOWS cases.</div>
</div>
<!-- Click 2: classifier + DMR -->
<div v-click="[2,3]" class="two-col">
    <img
      src="./Images/MOWS_SVM.png" class="absolute wide-figure"
    style="text-align: center; width: 47%; top: 30%; left: 25%; transform: translateX(-50%);"
    />
    <img
      src="./Images/MOWS_dmr.png" class="absolute wide-figure"
    style="text-align: center; width: 47%; top: 30%; left: 75%; transform: translateX(-50%);"
    />
    <div class="absolute figure-caption" style="text-align: center; width: 90%; top: 90%; left: 50%; transform: translateX(-50%);">[LEFT] ML models trained using discovery MOWS/Controls profiles. ENET (elastic net), KNN (k-nearest-neighbours), RF (random forest), SVM (Support Vector Machine). [RIGHT] Mean methylation of the top significant CpGs in <i>ZEB2/ZEB2-AS</i> region.</div>
</div>
<!-- Click 3: annotated DMR -->
<div v-click="[3,4]">
  <img
    src="./Images/MOWS_dmrAnnotTop.png" class="absolute wide-figure"
    style="text-align: center; width: 65%; top: 7%; left: 50%; transform: translateX(-50%);"
  />
  <img
    src="./Images/MOWS_dmrAnnotBot.png" class="absolute wide-figure"
    style="text-align: center; width: 65%; top: 57%; left: 50%; transform: translateX(-50%);"
  />
</div>

<div v-click="[4,5]">

  <img
    src="./Images/MOWS_NewNewbornEpi.png" class="absolute wide-figure"
    style="text-align: center; width: 100%; top: 20%; left: 50%; transform: translateX(-50%);"
  />
</div>

<div v-click="5">

  <img src="./Images/FINALpubl_MOWS.png" class="absolute wide-figure"
    style="text-align: center; width: 80%; top: 25%; left: 50%; transform: translateX(-50%);">

</div>

<div class="brand-footer">
  <img src="./Images/BRGE_Logo.png" class="footer-left" alt="BRGE logo" style="max-width: 100px;"/>
  <img src="./Images/ISGlobal_Logo.png" class="footer-right" alt="ISGlobal logo" style="max-width: 100px;"/>
</div>

---
layout: default
transition: fade
---

<div class="absolute" style="top: 1rem; left: 50%; transform: translateX(-50%); z-index: 5;">
  <SectionTimeline current="s3" />
</div>

<Countdown class="absolute top-2 right-2 z-0" :minutes="20" />

# Study 3: <span class="title-highlight">PMM2-CDG episignature</span>

<div class="lead-strip flex items-center gap-3" style="width: 100%">
  <div class="text-2xl text-[#f26b1d]" i-carbon-chemistry />
  <span>Glycosilation defect <span class="title-highlight">PMM2-CDG (<i>PMM2</i>)</span>. TriViae (SJD arrays) project.</span>
</div> 

<!-- Click 0: Introduction -->
<div class="two-col" v-click-hide="1">
  <div>
  <div class="relative" style="left: 50%; width:4 0%; transform: translateX(-50%); z-index: 5;">
      <div class="metric-card">
        <div class="metric-label">- Screened: 29 PMM2 (14 females, 15 males).<br>- Age: 10.7 &plusmn; 11.5.</div>
      </div>
    </div>
  </div>
  <div>
    <div class="relative" style="left: 50%; width:4 0%; transform: translateX(-50%); z-index: 5;">
      <div class="metric-card">
        <div class="metric-label">Highly heterogeneous syndrome.<br>2 PMM2-HIPKD phenotype cases.<br>1 carrier without phenotype.</div>
      </div>
    </div>
  </div>
</div>


<!-- Click 1: phenotype -->
<div v-click="[1,2]">
  <img
    src="./Images/PMM2GeneImg.png" class="absolute wide-figure"
    style="text-align: center; width: 900px; top: 25%; left: 50%; transform: translateX(-50%);"
  />
</div>
<!-- Click 2: variants -->
<div v-click="[2,3]">
  <img
    src="./Images/PMM2_variant_counts.png" class="absolute wide-figure"
    style="text-align: center; width: 100%; top: 25%; left: 50%; transform: translateX(-50%);"
  />
  <div class="absolute figure-caption" style="text-align: center; width: 90%; top: 93%; left: 50%; transform: translateX(-50%);"><i>PMM2</i> individual allele counts in the screened population and the variant effect across 3 different disease severity stages.</div>
</div>
<!-- Click 3: variants combinations -->
<div v-click="[3,4]">
  <img
    src="./Images/PMM2_variant_comb_counts.png" class="absolute wide-figure"
    style="text-align: center; width: 100%; top: 25%; left: 50%; transform: translateX(-50%);"
  />
  <div class="absolute figure-caption" style="text-align: center; width: 90%; top: 93%; left: 50%; transform: translateX(-50%);"><i>PMM2</i> genontype counts in the screened population and the combined variant effect across 3 different disease severity stages.</div>
</div>
<!-- Click 3: PCA -->
<div v-click="[4,5]" class="results-step">
  <img
    src="./Images/PMM2_PCA.png" class="absolute wide-figure"
    style="text-align: center; width: 100%; top: 25%; left: 50%; transform: translateX(-50%);"
  />
  <div class="absolute figure-caption" style="text-align: center; width: 90%; top: 93%; left: 50%; transform: translateX(-50%);"><i>PMM2</i> discovered episignature.</div>
</div>
<!-- Click 4: classifier -->
<div v-click="[5,6]" class="results-step">
  <img
    src="./Images/PMM2_SVM.png" class="absolute wide-figure"
    style="text-align: center; width: 100%; top: 25%; left: 50%; transform: translateX(-50%);"
  />
  <div class="absolute figure-caption" style="text-align: center; width: 90%; top: 93%; left: 50%; transform: translateX(-50%);"><i>PMM2</i> episignature SVM results.</div>
</div>

<!-- Click 5: HIPKD -->
<div v-click="[6,7]" class="results-step">
  <img
    src="./Images/PMM2_UCSC_genomicRegion.png" class="absolute wide-figure"
    style="text-align: center; width: 80%; top: 25%; left: 50%; transform: translateX(-50%);"
  />
  <div class="absolute" style="text-align: left; width: 90%; top: 45%;">Variant in <i>PMM2</i> promoter affects ZNF143 binding. Possible effect in <i>TMEM186</i> (bidirectional promoter).</div>
  <img
    src="./Images/PMM2_ZNFrole.png" class="absolute wide-figure"
    style="text-align: center; width: 55%; top: 52%; left: 50%; transform: translateX(-50%);"
  />
  <div class="absolute" style="text-align: center; width: 90%; top: 92%;">PMID: 36773065.</div></div>

<div v-click="7">
   <img src="./Images/FINALpubl_PMM2.png" class="absolute wide-figure"
    style="text-align: center; width: 80%; top: 35%; left: 50%; transform: translateX(-50%);">
</div>

<div class="brand-footer">
  <img src="./Images/BRGE_Logo.png" class="footer-left" alt="BRGE logo" style="max-width: 100px;"/>
  <img src="./Images/ISGlobal_Logo.png" class="footer-right" alt="ISGlobal logo" style="max-width: 100px;"/>
</div>

---
layout: default
transition: fade
---

<div class="absolute" style="top: 1rem; left: 50%; transform: translateX(-50%); z-index: 5;">
  <SectionTimeline current="s4" />
</div>

<Countdown class="absolute top-2 right-2 z-0" :minutes="20" />


<div v-click-hide="4">

# Study 4: <span class="title-highlight">Sotos sex-differences</span>


<div class="lead-strip flex items-center gap-3" style="width: 100%">
  <div class="text-2xl text-[#f26b1d]" i-carbon-chemistry />
  <span>Sotos (<i>NSD1</i>) sex-specific clinical delineation. TriViae (SJD arrays) project.</span>
</div> 

</div>

<!-- Click 1: XRa -->
<div v-click="[1,2]">
  <img
    src="./Images/Sotos_XRa.png" class="absolute wide-figure"
    style="text-align: center; width: 900px; top: 25%; left: 50%; transform: translateX(-50%);"
  />
</div>

<!-- Click 2: X chr compartments -->
<div v-click="[2,3]" class="two-col">
    <img
      src="./Images/Sotos_plt_methyGSE74432.png" class="absolute wide-figure"
    style="text-align: center; width: 47%; top: 30%; left: 25%; transform: translateX(-50%);"
    />
    <img
      src="./Images/Sotos_plt_methySJD.png" class="absolute wide-figure"
    style="text-align: center; width: 47%; top: 30%; left: 75%; transform: translateX(-50%);"
    />
    <div class="absolute figure-caption" style="text-align: center; width: 90%; top: 93%; left: 50%; transform: translateX(-50%);">[LEFT] GSE74432 dataset. [RIGHT] SJD dataset.</div>
</div>

<!-- Click 1: XRa -->
<div v-click="[3,4]">
  <img
    src="./Images/Sotos_SystRev.png" class="absolute wide-figure"
    style="text-align: center; width: 80%; top: 25%; left: 22%; transform: translateX(-50%);"
  />
  <img
    src="./Images/Sotos_StudyDesign.png" class="absolute wide-figure"
    style="text-align: center; width: 57%; top: 25%; left: 70%; transform: translateX(-50%);"
  />
</div>

<!-- Click 1: XRa -->
<div v-click="4">
  <img
    src="./Images/Sotos_Phenos_LogRegress2.png" class="absolute"
    style="text-align: center; width: 650px; top: 10%; left: 50%; transform: translateX(-50%);"
  />
</div>


<div class="brand-footer">
  <img src="./Images/BRGE_Logo.png" class="footer-left" alt="BRGE logo" style="max-width: 100px;"/>
  <img src="./Images/ISGlobal_Logo.png" class="footer-right" alt="ISGlobal logo" style="max-width: 100px;"/>
</div>

---
layout: default
transition: fade
---

<div class="absolute" style="top: 1rem; left: 50%; transform: translateX(-50%); z-index: 5;">
  <SectionTimeline current="new" />
</div>

<Countdown class="absolute top-2 right-2 z-0" :minutes="20" />

# Publications under review

<div v-click="[1,2]">
  <img src="./Images/FINALpubl_DDX3X.png" class="absolute wide-figure"
    style="text-align: center; width: 80%; top: 25%; left: 50%; transform: translateX(-50%);">
    <div class="absolute figure-caption" style="text-align: center; top: 90%; left: 50%; transform: translateX(-50%); width: 90%;"><i>DDX3X</i> episignature.<br>Under review in Genetics in Medicine.</div>
</div>

<div v-click="2">
  <img src="./Images/FINALpubl_BookChapt_XCI.png" class="absolute wide-figure"
    style="text-align: center; width: 80%; top: 17%; left: 50%; transform: translateX(-50%);">
  <img src="./Images/FINALpubl_BookChapt_Epis.png" class="absolute wide-figure"
    style="text-align: center; width: 80%; top: 50%; left: 50%; transform: translateX(-50%);">
    <div class="absolute figure-caption" style="text-align: center; top: 90%; left: 50%; transform: translateX(-50%); width: 90%;">Literature review about arrays/LR screening in RDs + literature review about available episignatures + episignature tutorial.<br>Epigenetics and Human Health book series (under review). </div>
</div>

<div class="brand-footer">
  <img src="./Images/BRGE_Logo.png" class="footer-left" alt="BRGE logo" style="max-width: 100px;"/>
  <img src="./Images/ISGlobal_Logo.png" class="footer-right" alt="ISGlobal logo" style="max-width: 100px;"/>
</div>

---
layout: default
transition: fade
---

<div class="absolute" style="top: 1rem; left: 50%; transform: translateX(-50%); z-index: 5;">
  <SectionTimeline current="new" />
</div>

<Countdown class="absolute top-2 right-2 z-0" :minutes="20" />

# Future congress

<div v-click="1">
  <img src="./Images/Imageomics_AltayPoster.png" class="absolute wide-figure"
    style="text-align: center; width: 80%; top: 17%; left: 50%; transform: translateX(-50%);">
  <img src="./Images/Imageomics_AlbertPoster.png" class="absolute wide-figure"
    style="text-align: center; width: 80%; top: 50%; left: 50%; transform: translateX(-50%);">
</div>

<div class="brand-footer">
  <img src="./Images/BRGE_Logo.png" class="footer-left" alt="BRGE logo" style="max-width: 100px;"/>
  <img src="./Images/ISGlobal_Logo.png" class="footer-right" alt="ISGlobal logo" style="max-width: 100px;"/>
</div>

---
layout: default
transition: fade
class: cover-slide
---

<div class="cover-content">
  <div class="cover-event">Team Meeting - 30 September 2026</div>

  <h1 class="cover-title">EPIFLARE: Episignatures and epigenetic monitoring in rare diseases</h1>

  <br>

  <div class="cover-meta">
    <div class="cover-author">
      Albert Alegret-García (ISGlobal)
    </div>
    <div class="cover-supervisors">
      <span>Supervised by</span>
      Juan R. González // Alejandro Cáceres (ISGlobal) || Luís A. Pérez-Jurado (UPF-IMIM)<br>
      Mercedes Serrano // Roser Urreizti // Dídac Casas (SJD) || Anna Esteve-Codina (CNAG)
    </div>
  </div>

  <div class="absolute cover-logos" style="width: 220px; bottom: 1rem; left: 1%; z-index: 5;">
    <img src="./Images/BRGE_Logo.png" alt="BRGE logo"/>
  </div>

  <div class="absolute cover-logos" style="width: 220px; bottom: 1rem; left: 90%; z-index: 5;">
    <img src="./Images/ISGlobal_Logo.png" alt="ISGlobal logo"/>
  </div>
</div>