---
# try also 'default' to start simple
theme: apple-basic
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: PyPSA-USA
info: Open source energy system optimization model
# apply UnoCSS classes to the current slide
class: pt-40
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable Comark Syntax: https://comark.dev/syntax/markdown
comark: true
layout: default
---

# PyPSA-USA Sector

## Open source Energy System Modeling for the United States

<!-- High-resolution data and optimization model energy transition analysis -->

<div class="pt-8 text-md opacity-60">
    <div>
        Kamran Tehranchi · Stanford · INES Research Group<br>
        <strong>Trevor Barnes</strong> · Simon Fraser University · ΔE+ Research Group<br>
        April 7th, 2026
    </div>
</div>

<div class="absolute right-0 bottom-0 flex items-center gap-4 p-4">
    <img src="/assets/s1/sfu.png" alt="Stanford" style="height: 40px;" />
    <img src="/assets/s1/stanford.png" alt="SFU" style="height: 40px;" />
</div>

<!--
Presenter Notes
-->

---
transition: fade-out
clicks: 4
---

# Sector Coupling

<div class="relative mt-10 h-80 w-115 mx-auto">
  <img v-if="$clicks === 0" src="/assets/s2/sector-1.png" class="absolute top-0 left-0 w-full" />
  <img v-if="$clicks === 1" src="/assets/s2/sector-2.png" class="absolute top-0 left-0 w-full" />
  <img v-if="$clicks === 2" src="/assets/s2/sector-3.png" class="absolute top-0 left-0 w-full" />
  <img v-if="$clicks === 3" src="/assets/s2/sector-4.png" class="absolute top-0 left-0 w-full" />
  <img v-if="$clicks >= 4" src="/assets/s2/sector-5.png" class="absolute top-0 left-0 w-full" />
</div>

<p v-if="$clicks >= 4" v-after class="mt-4 text-center text-gray-500">
  PyPSA-USA sector-coupled model.
</p>

<!--
presentation notes
-->


---
transition: slide-up
level: 2
---

# Case Study: New England
<!-- <p class="opacity-50 -mt-4 mb-10 text-lg">Evaluating regional decarbonization potential and system transition</p> -->
<div v-click>
  <h2 class="text-primary font-600 mb-4 border-b border-gray-200 pb-2">
    Research Question
  </h2>
  Evaluate regional decarbonization pathways for New England by 2030
</div>

<div class="grid grid-cols-2 gap-8 items-stretch p-6">

  <div v-click class="bg-gray-50 p-6 rounded-2xl border border-gray-100 shadow-sm flex flex-col justify-between">
    <h2 class="text-primary font-600 mb-6 border-b border-gray-200 pb-2 flex items-center gap-3">
      Model Requirements
    </h2>
    <div class="space-y-5 flex-grow">
      <div class="flex items-start gap-4">
        <div class="text-xl">🛢️</div>
        <div>
          <div class="font-bold">Sector Demand</div>
          <div class="text-sm opacity-70">Explicit modeling by fuel type</div>
        </div>
      </div>
      <div class="flex items-start gap-4">
        <div class="text-xl">🏗️</div>
        <div>
          <div class="font-bold">Brownfield Expansion</div>
          <div class="text-sm opacity-70">End-use technology integration</div>
        </div>
      </div>
      <div class="flex items-start gap-4">
        <div class="text-xl">🛑</div>
        <div>
          <div class="font-bold">Fuel & Policy Limits</div>
          <div class="text-sm opacity-70">Natural gas and build-rate constraints</div>
        </div>
      </div>
    </div>
  </div>

  <div v-click class="bg-gray-50 p-6 rounded-2xl border border-gray-100 shadow-sm">
    <h2 class="text-primary font-600 mb-6 border-b border-gray-200 pb-2 flex items-center gap-3">
      Result Metrics
    </h2>
    <div class="space-y-6">
      <div class="flex items-center gap-4">
        <div class="text-2xl">🌍</div>
        <div>
          <div class="font-bold">Emissions</div>
          <div class="text-xs opacity-60 uppercase tracking-wider">System & Sector Level</div>
        </div>
      </div>
      <div class="flex items-center gap-4">
        <div class="text-2xl">⚡️</div>
        <div>
          <div class="font-bold">Energy Flows</div>
          <div class="text-xs opacity-60 uppercase tracking-wider">Sankey-ready Data</div>
        </div>
      </div>
      <div class="flex items-center gap-4">
        <div class="text-2xl">💰</div>
        <div>
          <div class="font-bold">System Costs</div>
          <div class="text-xs opacity-60 uppercase tracking-wider">CAPEX & OPEX Analysis</div>
        </div>
      </div>
    </div>
  </div>
</div>


---
transition: slide-up
---

# Configuration Setup
<p class="opacity-50 -mt-4 mb-10 text-lg">Spatial and temporal configuration options</p>

<div class="grid grid-cols-[1.5fr_1fr] gap-12 mt-6 items-center">

  <div class="my-auto">
    <div class="text-xl leading-relaxed">

```yaml [config.default.yaml] {all|2|3-4|5,8|7|11,12|13,14|}
scenario:
  interconnect: [eastern]
  clusters: [6]
  simpl: [120]
  opts: [1h-TCT]
  ll: [v1.0]
  sector: "G"
  planning_horizons: [2030]

model_topology:
  transmission_network: 'reeds'
  topological_boundaries: 'reeds_zone'
  include:
    reeds_state: ['ME','MA','VT','NH','CT','RI']
```

</div>

</div>

<div class="flex justify-center">
<img src="/assets/s4/new-england.png" class="w-full rounded-2xl shadow-lg border border-gray-100" />
</div>

</div>

<style>
/* This ensures the code block inside your custom grid scales up */
.shiki {
font-size: 1rem !important;
line-height: 1.2 !important;
}
</style>

---
transition: slide-up
---

# Renewable Capacity Factors
<p class="opacity-50 -mt-4 mb-10 text-lg">Spatial distribution of solar and wind potential in New England</p>

<div class="grid grid-cols-2 gap-12 items-center">

  <div class="flex flex-col items-center">
    <div class="bg-gray-50 p-4 rounded-3xl border border-gray-100 shadow-sm w-full">
      <img src="/assets/s5/solar_cf.png" class="w-full rounded-2xl" />
    </div>
    <h3 class="mt-4 font-600 text-primary flex items-center gap-2">
      ☀️ Solar PV (AC)
    </h3>
    <p class="text-sm opacity-60 italic text-center">Avg. Capacity Factor by Node</p>
  </div>

  <div class="flex flex-col items-center">
    <div class="bg-gray-50 p-4 rounded-3xl border border-gray-100 shadow-sm w-full">
      <img src="/assets/s5/wind_cf.png" class="w-full rounded-2xl" />
    </div>
    <h3 class="mt-4 font-600 text-primary flex items-center gap-2">
      🌬️ Onshore Wind
    </h3>
    <p class="text-sm opacity-60 italic text-center">Avg. Capacity Factor by Node</p>
  </div>

</div>

---
transition: slide-up
layout: default
dragPos:
  square: 56,517,345,345
---

# Demand
<p class="opacity-50 -mt-4 mb-8 text-lg">Service Sector Load Profiles</p>

<div class="grid grid-cols-2 gap-10 h-[440px]">

  <div class="flex flex-col justify-top gap-10 h-full p-0 pt-10">
    <div class="custom-code">
```yaml [config.default.yaml] {1,3,6}
demand: 
  profile: efs # not used
  scenario: 
    efs_case: reference  # not used
    efs_speed: moderate  # not used
    aeo: reference
```
</div>

<div class="flex justify-evenly items-center bg-gray-50 p-6 rounded-2xl border border-gray-100 shadow-sm">
  <a href="https://resstock.nrel.gov/" target="_blank" class="transition-transform hover:scale-110">
    <img src="/assets/s6/resstock.png" class="h-10 rounded bg-white px-3 border border-gray-200 shadow-sm" alt="ResStock" />
  </a>
  <a href="https://comstock.nrel.gov/" target="_blank" class="transition-transform hover:scale-110">
    <img src="/assets/s6/comstock.png" class="h-10 rounded bg-white px-3 border border-gray-200 shadow-sm" alt="ComStock" />
  </a>
</div>

</div>

<div class="flex flex-col justify-between h-full gap-4 -mt-30">
<div class="bg-gray-50 p-2 rounded-2xl border border-gray-100 shadow-sm flex-1 flex flex-col justify-center">
<img src="/assets/s6/res-profile.png" class="w-full object-contain rounded-xl max-h-[220px]" alt="Residential Load" />
<!-- <p class="text-center text-[14px] opacity-60 mt-0">Residential Profile</p> -->
</div>
<div class="text-center text-[11px] opacity-40 uppercase tracking-widest -mt-2">Massachusetts Residential Profile</div>

<div class="bg-gray-50 p-2 rounded-2xl border border-gray-50 shadow-sm flex-1 flex flex-col -mt-2 justify-center">
  <img src="/assets/s6/com-profile.png" class="w-full object-contain rounded-xl max-h-[220px]" alt="Commercial Load" />
  <!-- <p class="text-center text-[14px] opacity-60 mt-0">Commercial Profile</p> -->
</div>
<div class="text-center text-[11px] opacity-40 uppercase tracking-widest -mt-2">Massachusetts Commercial Profile</div>

</div>

</div>

<style>
.shiki {
font-size: 1rem !important;
line-height: 1.4 !important;
border: 1px solid #e5e7eb !important;
}
</style>

---
transition: slide-up
layout: default
---

# Demand
<p class="opacity-50 -mt-4 mb-8 text-lg">Service Sector Load Profiles</p>

<div class="flex flex-col items-center justify-center h-[400px]">
  
  <div class="bg-gray-50 p-4 rounded-3xl border border-gray-100 shadow-sm max-w-[700px]">
    <img src="/assets/s7/service-load.png" class="w-full rounded-2xl" alt="Service Sector Load" />
  </div>

  <p class="text-center text-[10px] opacity-40 mt-4 uppercase tracking-widest leading-none">
    Service sector load in New England
  </p>

</div>

---
transition: slide-up
layout: default
---

# Demand
<p class="opacity-50 -mt-4 mb-8 text-lg">Transportation Sector Load Profiles</p>

<div class="grid grid-cols-[0.75fr_1.25fr] gap-10 h-[460px]">

  <div class="flex flex-col justify-start gap-10 h-full pt-10">
    <div class="custom-code">
```yaml [config.default.yaml] {1,3-6}
demand: 
  profile: efs # not used
  scenario: 
    efs_case: reference 
    efs_speed: moderate 
    aeo: reference
```

</div>

<div class="flex flex-col items-center justify-center text-center">
  <span class="text-[10px] font-bold uppercase tracking-widest opacity-40 mb-3 max-w-[200px]">
    NLR Electrification Future Study
  </span>
  <a href="https://zenodo.org/records/15295016" target="_blank" class="transition-transform hover:scale-110">
    <img src="/assets/s8/efs.png" class="h-20 rounded-lg bg-white px-4 py-2 border border-gray-100 shadow-md" alt="NLR EFS" />
  </a>
</div>

</div>

<div class="flex flex-col justify-center items-center h-full">
<div class="bg-gray-50 p-4 -mt-30 rounded-3xl border border-gray-100 shadow-sm w-full max-w-[600px]">
<img src="/assets/s8/ev-profiles.png" class="w-full rounded-2xl" alt="EV Load Profiles" />
</div>

<p class="text-center text-[10px] opacity-40 mt-4 uppercase tracking-widest leading-tight max-w-[500px]">
  Electric vehicle load profiles. Gray lines are hourly profiles over the year. The blue line is the average profile over the year. <br> (a) Light-Duty (b) Medium-Duty (c) Heavy-Duty (d) Buses
</p>

</div>

</div>

<style>
.shiki {
font-size: 0.9rem !important;
line-height: 1.3 !important;
border: 1px solid #e5e7eb !important;
}
</style>










---
transition: slide-up
layout: default
---

# Load Dissagregation

<div class="grid grid-cols-2 gap-16 mt-12 items-center">

  <div class="flex flex-col h-full justify-top pl-4 mt-4">
    <h2 class="text-primary font-600 mb-4 border-b border-gray-200 pb-2 flex items-center gap-3 text-xl">
      Population-based Disaggregation
    </h2>
    <ul class="space-y-6 list-none pl-0">
      <li class="flex items-start gap-4">
        <div class="mt-2.5 h-2.5 w-2.5 rounded-full bg-blue-500 shrink-0" />
        <div>
          <strong class="text-lg">Residential</strong><br>
        </div>
      </li>
      <li class="flex items-start gap-4">
        <div class="mt-2.5 h-2.5 w-2.5 rounded-full bg-blue-500 shrink-0" />
        <div>
          <strong class="text-lg">Commercial</strong><br>
        </div>
      </li>
      <li class="flex items-start gap-4">
        <div class="mt-2.5 h-2.5 w-2.5 rounded-full bg-blue-500 shrink-0" />
        <div>
          <strong class="text-lg">Transport</strong><br>
        </div>
      </li>
    </ul>
    <h2 class="text-primary font-600 mb-4 border-b border-gray-200 pb-2 flex items-center gap-3 text-xl">
      Emissions-based Disaggregation
    </h2>
    <ul class="space-y-6 list-none pl-0">
      <li class="flex items-start gap-4">
        <div class="mt-2.5 h-2.5 w-2.5 rounded-full bg-blue-500 shrink-0" />
        <div>
          <strong class="text-lg">Industrial</strong><br>
        </div>
      </li>
    </ul>
  </div>

  <div class="flex flex-col items-center justify-center">
    <div class="bg-gray-50 p-3 rounded-3xl border border-gray-100 shadow-sm w-full -mt-15">
      <img src="/assets/s/urbanization.png" class="w-full rounded-2xl" alt="Urbanization Map" />
    </div>
    <p class="text-center text-[11px] opacity-40 mt-2 uppercase tracking-widest leading-none">
      New England urbanization rates
    </p>
  </div>

</div>

