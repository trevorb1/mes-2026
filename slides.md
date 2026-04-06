---
theme: apple-basic
background: https://cover.sli.dev
title: PyPSA-USA
info: Open source energy system optimization model
class: pt-40
transition: slide-up
comark: true
layout: default
---

# PyPSA-USA Sector

## Open source Energy System Modeling for the United States

<!-- High-resolution data and optimization model energy transition analysis -->

<img 
  src="/assets/s1/pypsa-logo.png" 
  class="absolute object-cover opacity-10 -mt-50 pl-125" 
/>

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
transition: slide-up
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
  <h2 class="text-primary font-600 mb-4 border-b border-gray-10 pb-2">
    Research Question
  </h2>
  Evaluate regional decarbonization pathways for New England by 2030
</div>

<div class="grid grid-cols-2 gap-8 items-stretch p-6">

  <div v-click class="bg-gray-50 p-6 rounded-2xl border border-gray-10 shadow-sm flex flex-col justify-between">
    <h2 class="text-primary font-600 mb-6 border-b border-gray-10 pb-2 flex items-center gap-3">
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

  <div v-click class="bg-gray-50 p-6 rounded-2xl border border-gray-10 shadow-sm">
    <h2 class="text-primary font-600 mb-6 border-b border-gray-10 pb-2 flex items-center gap-3">
      Result Metrics
    </h2>
    <div class="space-y-6">
      <div class="flex items-center gap-4">
        <div class="text-2xl">🌍</div>
        <div>
          <div class="font-bold">Emissions</div>
          <div class="text-sm opacity-70">System & Sector Level</div>
        </div>
      </div>
      <div class="flex items-center gap-4">
        <div class="text-2xl">⚡️</div>
        <div>
          <div class="font-bold">Energy Flows</div>
          <div class="text-sm opacity-70">Sankey-ready Data</div>
        </div>
      </div>
      <div class="flex items-center gap-4">
        <div class="text-2xl">💰</div>
        <div>
          <div class="font-bold">System Costs</div>
          <div class="text-sm opacity-70">CAPEX & OPEX Analysis</div>
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

```yaml [config.default.yaml] {0|1,2|1,3-4|1,5,8|1,7|10,11,12|10,13,14|all}
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

<div class="flex justify-center -mt-20">
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
hide: true
---

# Renewable Capacity Factors
<p class="opacity-50 -mt-4 mb-10 text-lg">Spatial distribution of solar and wind potential in New England</p>

<div class="grid grid-cols-2 gap-12 items-center">

  <div class="flex flex-col items-center">
    <div class="p-4 rounded-3xl w-full">
      <img src="/assets/s5/solar_cf.png" class="w-full rounded-2xl" />
    </div>
  </div>

  <div class="flex flex-col items-center">
    <div class="p-4 rounded-3xl w-full">
      <img src="/assets/s5/wind_cf.png" class="w-full rounded-2xl" />
    </div>
  </div>

</div>

---
transition: slide-up
layout: default
---

# Demand Profiles
<p class="opacity-50 -mt-4 mb-8 text-lg">Service Sector Load Profiles</p>

<div class="grid grid-cols-2 gap-10 h-[440px]">

  <div class="flex flex-col justify-top gap-10 h-full p-0 pt-10">
    <div v-click class="custom-code">
```yaml [config.default.yaml] {1,3}
demand: 
  profile: efs  # not used
  scenario: 
    efs_case: reference  # not used
    efs_speed: moderate  # not used
    aeo: reference  # not used
```
</div>

<div v-click class="flex justify-evenly items-center bg-gray-50 p-6 rounded-2xl border border-gray-10 shadow-sm">
  <a href="https://resstock.nrel.gov/" target="_blank" class="transition-transform hover:scale-110">
    <img src="/assets/s6/resstock.png" class="h-10 rounded bg-white px-3 border border-gray-10 shadow-sm" alt="ResStock" />
  </a>
  <a href="https://comstock.nrel.gov/" target="_blank" class="transition-transform hover:scale-110">
    <img src="/assets/s6/comstock.png" class="h-10 rounded bg-white px-3 border border-gray-10 shadow-sm" alt="ComStock" />
  </a>
</div>

</div>

<div v-click class="flex flex-col justify-between h-full gap-4 -mt-30">
<div class="p-4 rounded-3xl w-full">
<img src="/assets/s6/res-profile.png" class="w-full object-contain rounded-xl max-h-[220px]" alt="Residential Load" />
<!-- <p class="text-center text-[14px] opacity-60 mt-0">Residential Profile</p> -->
</div>
<div class="text-center text-[11px] opacity-40 uppercase tracking-widest -mt-8">Massachusetts Residential Profile</div>

<div class="p-4 rounded-3xl w-full">
  <img src="/assets/s6/com-profile.png" class="w-full object-contain rounded-xl max-h-[220px]" alt="Commercial Load" />
  <!-- <p class="text-center text-[14px] opacity-60 mt-0">Commercial Profile</p> -->
</div>
<div class="text-center text-[11px] opacity-40 uppercase tracking-widest -mt-8">Massachusetts Commercial Profile</div>

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

# Demand Profiles
<p class="opacity-50 -mt-4 mb-8 text-lg">Service Sector Load Profiles</p>

<div class="flex flex-col items-center justify-center h-[400px]">
  
  <div class="p-4 rounded-3xl max-w-[700px]">
    <img src="/assets/s7/service-load.png" class="w-full rounded-2xl" alt="Service Sector Load" />
  </div>

  <p class="text-center text-[11px] opacity-40 mt-4 uppercase tracking-widest leading-none">
    Service sector load in New England
  </p>

</div>

---
transition: slide-up
layout: default
---

# Demand Profiles
<p class="opacity-50 -mt-4 mb-8 text-lg">Transportation Sector Load Profiles</p>

<div class="grid grid-cols-[0.75fr_1.25fr] gap-10 h-[460px]">

  <div v-click class="flex flex-col justify-start gap-10 h-full pt-10">
    <div class="custom-code">
```yaml [config.default.yaml] {1,3-5}
demand: 
  profile: efs # not used
  scenario: 
    efs_case: reference 
    efs_speed: moderate 
    aeo: reference # not used
```

</div>

<div class="flex flex-col items-center justify-center text-center">
  <span class="text-[11px] font-bold uppercase tracking-widest opacity-40 mb-3 max-w-[200px]">
    NLR Electrification Future Study
  </span>
  <a href="https://zenodo.org/records/15295016" target="_blank" class="transition-transform hover:scale-110">
    <img src="/assets/s8/efs.png" class="h-20 rounded-lg bg-white px-4 py-2 border border-gray-10 shadow-md" alt="NLR EFS" />
  </a>
</div>

</div>

<div v-click class="flex flex-col justify-center items-center h-full">
<div class="p-4 -mt-30 rounded-3xl w-full max-w-[650px]">
<img src="/assets/s8/ev-profiles.png" class="w-full rounded-2xl" alt="EV Load Profiles" />
</div>

<p class="text-center text-[11px] opacity-40 mt-4 uppercase tracking-widest leading-tight max-w-[500px]">
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
dragPos:
  square: 56,517,345,345
---

# Demand Profiles
<p class="opacity-50 -mt-4 mb-8 text-lg">Industrial Sector Load Profiles</p>

<div class="grid grid-cols-[0.8fr_1.20fr] gap-10 h-[440px]">

  <div class="flex flex-col justify-top gap-10 h-full p-0 pt-10">
    <div class="custom-code">
```yaml [config.default.yaml] {1,3}
demand: 
  profile: efs # not used
  scenario: 
    efs_case: reference  # not used
    efs_speed: moderate  # not used
    aeo: reference  # not used
```
</div>

<div class="grid grid-cols-3 gap-4 items-center bg-gray-50 p-6 rounded-2xl border border-gray-100 shadow-sm">
  
  <a href="https://loadshape.epri.com/enduse" target="_blank" class="flex justify-center transition-transform hover:scale-110">
    <img src="/assets/s9/epri.png" class="h-8 w-auto object-contain bg-white px-3 py-1 rounded border border-gray-100 shadow-sm" alt="EPRI" />
  </a>

  <a href="https://www.eia.gov/consumption/manufacturing/" target="_blank" class="flex justify-center transition-transform hover:scale-110">
    <img src="/assets/s9/eia.png" class="h-8 w-auto object-contain bg-white px-3 py-1 rounded border border-gray-100 shadow-sm" alt="EIA" />
  </a>

  <a href="https://data.nlr.gov/submissions/97" target="_blank" class="flex justify-center transition-transform hover:scale-110">
    <img src="/assets/s9/nlr.png" class="h-8 w-auto object-contain bg-white px-3 py-1 rounded border border-gray-100 shadow-sm" alt="NLR" />
  </a>

</div>

</div>

<div class="flex flex-col justify-center gap-0 -mt-20">
<div class="px-4 py-4 rounded-2xl">
<img src="/assets/s9/load.png" class="w-full object-contain rounded-xl max-h-[320px]" alt="Industrial Load" />
</div>
<div class="text-center text-[11px] opacity-40 uppercase tracking-widest ">Massachusetts Industrial Profile</div>

</div>

</div>

<style>
.shiki {
font-size: 0.9rem !important;
line-height: 1 !important;
border: 1px solid #e5e7eb !important;
}
</style>


---
transition: slide-up
layout: default
---

# Demand Dissagregation

<div class="grid grid-cols-2 gap-16 mt-12 items-center">

  <div class="flex flex-col h-full justify-top pl-4 mt-4">
    <h2 class="text-primary font-600 mb-4 border-b border-gray-10 pb-2 flex items-center gap-3 text-xl">
      Population-based disaggregation
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
    <h2 class="text-primary font-600 mb-4 border-b border-gray-10 pb-2 flex items-center gap-3 text-xl">
      Emissions-based disaggregation
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
    <div class="p-3 rounded-3xl -mt-15">
      <img src="/assets/s10/urbanization.png" class="w-full rounded-2xl" alt="Urbanization Map" />
    </div>
    <p class="text-center text-[11px] opacity-40 mt-2 uppercase tracking-widest leading-none">
      New England urbanization rates
    </p>
  </div>

</div>

---
transition: slide-up
layout: default
---

# Demand Magnitudes
<p class="opacity-50 -mt-4 mb-8 text-lg">Scaling Load Profiles</p>

<div class="grid grid-cols-[0.8fr_1.20fr] gap-10 h-[440px]">

  <div v-click class="flex flex-col justify-top gap-10 h-full p-0 pt-10">
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

<div class="flex flex-col items-center justify-center text-center">
  <span class="text-[11px] font-bold uppercase tracking-widest opacity-40 mb-3 max-w-[200px]">
    Annual Energy Outlook
  </span>
  <a href="https://www.eia.gov/outlooks/aeo/" target="_blank" class="transition-transform hover:scale-110">
    <img src="/assets/s9/eia.png" class="h-20 rounded-lg bg-white px-4 py-2 border border-gray-10 shadow-md" alt="EIA" />
  </a>
</div>

</div>

<div v-click class="flex flex-col justify-center gap-0 -mt-20">
<div class="rounded-2xl">
<img src="/assets/s11/aeo-commercial.png" class="w-full object-contain rounded-xl max-h-[450px]" alt="Industrial Load" />
</div>
<div class="text-center text-[11px] opacity-40 uppercase tracking-widest mt-2">Annual Energy Outlook Commerical Energy Growth</div>

</div>

</div>

<style>
.shiki {
font-size: 0.9rem !important;
line-height: 1 !important;
border: 1px solid #e5e7eb !important;
}
</style>

---
transition: slide-up
layout: default
---

# Technology Representation
<p class="opacity-50 -mt-4 mb-8 text-lg">Service Sector</p>

<div class="grid grid-cols-[0.8fr_1.20fr] gap-10 h-[440px]">

  <div class="flex flex-col justify-top gap-10 h-full p-0 pt-10">
    <div class="custom-code">
```yaml [config.sector.yaml] {0|1-3|1,4,5|1,4-11|1,4,5,12-15|1,4,5,12,15|all}
sector:
  heating:
    heat_pump_sink_T: 55.
  service_sector: 
    technologies:
      space_heating:
        elec_furnace: true
        gas_furnace: true
        oil_furnace: true
        heat_pump: true
        air_con: true
      water_heating: 
        elec_water_tank: true 
        gas_water_tank: true
        oil_water_tank: false
```
</div>

</div>

<div class="flex flex-col justify-center gap-0 -mt-20">
<div v-click="1" class="px-4 py-4 rounded-2xl">
<img src="/assets/s12/cop.png" class="w-full object-contain rounded-xl max-h-[280px]" alt="Industrial Load" />
</div>
<div v-click="1" class="text-center text-[11px] opacity-40 uppercase tracking-widest mt-2">New England (a) Air-Source Heat Pump and <br> (b) Ground-Source Heat Pump COPs</div>

<div v-click="2" class="grid grid-cols-2 gap-20 items-center bg-gray-50 p-6 rounded-2xl border border-gray-100 shadow-sm" mt-10>

  <a href="https://www.eia.gov/consumption/residential/" target="_blank" class="flex justify-center transition-transform hover:scale-110">
    <span>→</span> EIA RECS
  </a>

  <a href="https://www.eia.gov/consumption/commercial/" target="_blank" class="flex justify-center transition-transform hover:scale-110">
    <span>→</span> EIA CECS
  </a>

</div>

</div>

</div>

<style>
.shiki {
font-size: 0.75rem !important;
line-height: 1 !important;
border: 1px solid #e5e7eb !important;
}
</style>

---
transition: slide-up
layout: default
---

# Technology Representation
<p class="opacity-50 -mt-4 mb-8 text-lg">Transportation Sector</p>

<div class="grid grid-cols-[0.8fr_1.20fr] gap-10 h-[440px]">

  <div class="flex flex-col justify-top gap-10 h-full p-0 pt-10">
    <div class="custom-code">
```yaml [config.sector.yaml] {0|1,2|1,2|1-3|1,2,4|1,2,5|1,2,6-9|all}
sector:
  transport_sector:
    dynamic_costs: True 
    ev_policy: "ev_policy.csv"
    must_run_evs: True
    modes:
      rail: true
      air: true
      boat: true
```
</div>

<div v-click=2 class="flex flex-row items-center justify-center gap-6">
  <span class="text-[11px] font-bold uppercase tracking-widest opacity-40 text-right max-w-[120px] leading-tight">
    NLR Electrification <br> Future Study
  </span>

  <a href="https://zenodo.org/records/15295016" target="_blank" class="transition-transform hover:scale-110 shrink-0">
    <img src="/assets/s8/efs.png" class="h-16 rounded-lg bg-white px-4 py-2 border border-gray-100 shadow-md" alt="NLR EFS" />
  </a>
</div>

</div>

<div v-click=2 class="flex flex-col justify-center gap-0 -mt-20">
<div class="px-4 py-4 rounded-2xl">
<img src="/assets/s13/transport-res.png" class="w-full object-contain rounded-xl max-h-[320px]" alt="Industrial Load" />
</div>
<div class="text-center text-[11px] opacity-40 uppercase tracking-widest mt-2">Road transportation technology representation</div>

</div>

</div>

<style>
.shiki {
font-size: 0.75rem !important;
line-height: 1 !important;
border: 1px solid #e5e7eb !important;
}
</style>

---
transition: slide-up
layout: default
---

# Technology Representation
<p class="opacity-50 -mt-4 mb-8 text-lg">Industrial Sector</p>

<div class="grid grid-cols-[0.8fr_1.20fr] gap-10 h-[440px]">

  <div class="flex flex-col justify-top gap-10 h-full p-0 pt-10">
    <div class="custom-code">
```yaml [config.sector.yaml] {0|1,2|1-6|1,2,7|1,2,8|all}
sector:
  industrial_sector: 
    technologies: 
      gas_furnace: true
      coal_furnace: true
      heat_pump: true
    dynamic_costs: True
    min_fossil_generation: 66 # percent
```
</div>

</div>

<div v-click=2 class="flex flex-col justify-center gap-0 -mt-20">
<div class="px-4 py-4 rounded-2xl">
<img src="/assets/s14/res.png" class="w-full object-contain rounded-xl max-h-[320px]" alt="Industrial Load" />
</div>
<div class="text-center text-[11px] opacity-40 uppercase tracking-widest mt-2">Industry technology representation</div>

</div>

</div>

<style>
.shiki {
font-size: 0.75rem !important;
line-height: 1 !important;
border: 1px solid #e5e7eb !important;
}
</style>

---
transition: slide-up
---

# Technology Representation
<p class="opacity-50 -mt-4 mb-8 text-lg">Natural Gas</p>

<div class="grid grid-cols-[2fr_1fr] gap-4 h-[400px] mt-10">

  <div class="flex items-center justify-center relative">
    <img v-click="1" src="/assets/s15/sector-1.png" v-if="$clicks === 1" class="w-full object-contain max-h-[350px]" />
    <img v-click="2" src="/assets/s15/sector-2.png" v-if="$clicks === 2" class="w-full object-contain max-h-[350px]" />
    <img v-click="3" src="/assets/s15/sector-3.png" v-if="$clicks === 3" class="w-full object-contain max-h-[350px]" />
    <img v-click="4" src="/assets/s15/sector-4.png" v-if="$clicks >= 4" class="w-full object-contain max-h-[350px]" />
  </div>

  <div v-click="5" class="flex items-center justify-center -mt-40">
    <img src="/assets/s15/sources.png" class="w-full object-contain max-h-[350px]" alt="Sources" />
  </div>
</div>


---
transition: slide-up
layout: default
---

# Boundary Conditions
<p class="opacity-50 -mt-4 mb-8 text-lg">Electrical Trade</p>

<div class="grid grid-cols-[0.8fr_1.20fr] gap-10 h-[440px]">

  <div class="flex flex-col justify-top gap-10 h-full p-0 pt-10">
    <div class="custom-code">
```yaml [config.default.yaml] {0|1,2,3,9,10|1,2,4,9,11|1,2,6,7,9,12,13|1,2,6,7,9,12,13|1,2,8,9,14|1,2,5|all}
electricity:
  imports:
    enable: true 
    costs: wholesale # wholesale|carrier|float
    co2_emissions: 0.384 # TCO2 / MWh
    volume_limit: 20 # percentage
    balancing_period: year # day|week|month|year 
    capacity_limit: true 
  exports:
    enable: true 
    costs: wholesale 
    volume_limit: 5 
    balancing_period: year 
    capacity_limit: true 
```
</div>

</div>

<div v-click=4 class="flex flex-col justify-center gap-0 -mt-35">
<div class="bg-gray-50 px-4 py-4 rounded-2xl border border-gray-100 shadow-sm">
<img src="/assets/s16/neiso.png" class="w-full object-contain rounded-xl max-h-[320px]" alt="Industrial Load" />
</div>
<div class="text-center text-[11px] opacity-40 uppercase tracking-widest mt-2">New England ISO Energy Mix</div>

<div class="flex flex-row items-center justify-center gap-6 mt-10">
  <a href="https://www.iso-ne.com/" target="_blank" class="transition-transform hover:scale-110 shrink-0">
    <img src="/assets/s16/ne-logo.png" class="h-16 rounded-lg bg-white px-4 py-2 border border-gray-100 shadow-md" alt="ISO-NE" />
  </a>
  <a href="https://catalyst.coop/pudl/" target="_blank" class="transition-transform hover:scale-110 shrink-0">
    <img src="/assets/s16/pudl.png" class="h-16 rounded-lg bg-white px-4 py-2 border border-gray-100 shadow-md" alt="ISO-NE" />
  </a>
</div>

</div>

</div>

<style>
.shiki {
font-size: 0.75rem !important;
line-height: 1 !important;
border: 1px solid #e5e7eb !important;
}
</style>

---
transition: slide-up
layout: default
---

# Boundary Conditions
<p class="opacity-50 -mt-4 mb-8 text-lg">Natural Gas Trade</p>

<div class="grid grid-cols-[0.8fr_1.20fr] gap-10 h-[440px]">

  <div class="flex flex-col justify-top gap-10 h-full p-0 pt-10">
    <div class="custom-code">
```yaml [config.sector.yaml]{0|1,2|1,2|1-8|1,2,9,10|1,2,11|1,2,12|1,13-16|all}
sector:
  natural_gas:
    imports: # percentage
      min: 0
      max: 1.2
    exports: # percentage
      min: 0.8
      max: 1.2
    cyclic_storage: true
    standing_loss: 0 # per unit
    marginal_cost_multiplier: 1 # per unit
    existing_pipeline_multiplier: 1.2 # per unit
  methane:
    upstream_leakage_rate: 0.02 # per unit 
    downstream_leakage_rate: 0.02 # per unit 
    gwp: 0 
```
</div>

</div>

<div v-click=2 class="flex flex-col justify-center gap-0 -mt-35">
<div class="px-4 py-4 rounded-2xl">
<img src="/assets/s17/ng_connections.png" class="w-full object-contain rounded-xl max-h-[400px]" alt="Natural Gas Connections" />
</div>
<div class="text-center text-[11px] opacity-40 uppercase tracking-widest mt-2">New England Natural Gas Pipeline COnnections</div>

</div>

</div>

<style>
.shiki {
font-size: 0.75rem !important;
line-height: 1 !important;
border: 1px solid #e5e7eb !important;
}
</style>

---
transition: slide-up
layout: two-cols
---

# Policies
<p class="opacity-50 -mt-4 mb-8 text-lg">Additional Constraints</p>

::left::

<div class="custom-code">

```ts{0|1-4,8-13}
.
└── pypsa-usa/
    ├── workflow/
    │   ├── config/
    │   │   ├── config.defaul.yaml
    │   │   ├── config.sector.yaml
    │   │   ├── ...
    │   │   └── policy_constraints/
    │   │       ├── technology_capacity_targets.csv
    │   │       ├── ev_policy.csv
    │   │       ├── sector_co2_limit.csv
    │   │       ├── portfolio_standards.csv
    │   │       └── ...
    │   ├── resources/
    │   ├── results/
    │   ├── scripts/
    │   └── rules
    └── docs/
```
</div>

::right::

<div class="flex flex-col h-full justify-center pl-4">
<div v-click class="bg-gray-50 p-6 rounded-2xl border border-gray-10 shadow-sm flex flex-col">
<h2 class="text-primary font-600 mb-6 border-b border-gray-10 pb-2 flex items-center gap-3 text-xl">
Full User Customization
</h2>
    <div class="space-y-6">
      <div class="flex items-start gap-4">
        <div class="text-2xl">🔧</div>
        <div>
          <div class="font-bold text-lg">Modify existing constraints</div>
          <div class="text-sm opacity-70">Adjust parameters in config files</div>
        </div>
      </div>
      <div class="flex items-start gap-4">
        <div class="text-2xl">➕</div>
        <div>
          <div class="font-bold text-lg">Add new constraints</div>
          <div class="text-sm opacity-70">Define custom policy limits for specific regions</div>
        </div>
      </div>
      <div class="flex items-start gap-4">
        <div class="text-2xl">📊</div>
        <div>
          <div class="font-bold text-lg">Include new data</div>
          <div class="text-sm opacity-70">Integrate external datasets into the optimization</div>
        </div>
      </div>
    </div>
</div>

</div>


---
transition: slide-up
layout: default
---

# Policies
<p class="opacity-50 -mt-4 mb-8 text-lg">TCT and EV Policy</p>

<div v-click=1 class="mb-10 mt-10">

```csv [technology_capacity_targets.csv]{0|0|1|1-6|1,7|all}
name,planning_horizon,region,carrier,min,max
solar,2030,"ME,MA,VT,NH,CT,RI",solar,,8566
wind,2030,"ME,MA,VT,NH,CT,RI","onwind, offwind_floating",,4351
ocgt,2030,"ME,MA,VT,NH,CT,RI",OCGT,,10312
ccgt,2030,"ME,MA,VT,NH,CT,RI","CCGT, CCGT-95CCS, CCGT-97CCS",,35465
battery,2030,"ME,MA,VT,NH,CT,RI","4hr_battery_storage, 8hr_battery_storage",,1606
oil_furnace,2030,"ME,MA,VT,NH,CT,RI","com-total-space-oil-furnace, res-total-space-oil-furnace",,90783
```

</div>
<div v-click=5>

```csv [ev_policy.csv]{0|1|all}
,light_duty,med_duty,heavy_duty,bus
2030,34.18,7.27,6.11,34.2

```

</div>

<style>
/* Targets all code blocks on this specific slide */
.shiki {
  font-size: 14px !important; 
  line-height: 1.2 !important;
}

/* Optional: reduce the padding inside the code block to save space */
.shiki pre {
  padding: 8px !important;
}
</style>


---
transition: slide-up
layout: default
---

# Run the Model!
<p class="opacity-50 -mt-4 mb-8 text-lg">Navigating results</p>

<div class="grid grid-cols-[1.2fr_0.8fr] gap-10 h-[460px] items-center">

  <div class="flex flex-col justify-start gap-6 -mt-15">
    <div v-click=1 class="large-code">
      <span class="text-[11px] uppercase tracking-widest opacity-40 mb-1 block">1. Execute Workflow</span>
```bash 
mamba activate pypsa-usa
snakemake -j1 --configfile config/config.default.yaml
```
</div>

<div v-click=3 class="large-code">
  <span class="text-[11px] uppercase tracking-widest opacity-40 mb-1 block">3. Inspect Results</span>
```python 
import pypsa
n = pypsa.Network("*.nc")
# see pypsa.Network.statistics
```
  </div>
  </div>


<div v-click=2 class="flex flex-col justify-center h-full pt-4 -mt-40">
<div class="tree-code">
      <span class="text-[11px] uppercase tracking-widest opacity-40 mb-1 block">2. Standard PyPSA-USA output structure</span>
```ts{6-23}
.
└── pypsa-usa/
    ├── workflow/
    │   ├── config/
    │   ├── resources/
    │   ├── results/
    │   │   └── <scenario>/
    │   │       ├── networks/
    │   │       │   └── *.nc
    │   │       ├── configs/
    │   │       └── figures/
    │   │           ├── CT/
    │   │           │   ├── capacity
    │   │           │   ├── emissions
    │   │           │   ├── production
    │   │           │   ├── sankey
    │   │           │   └── natural_gas
    │   │           ├── MA/
    │   │           ├── ME/
    │   │           ├── NH/
    │   │           ├── RI/
    │   │           ├── VT/
    │   │           └── System/
    │   ├── scripts/
    │   └── rules
    └── docs/
```
</div>

</div>

</div>

<style>
/* Larger font for the commands */
.large-code .shiki {
font-size: 1rem !important;
line-height: 1.4 !important;
border: 1px solid #e5e7eb !important;
background-color: #f9fafb !important;
padding: 1rem !important;
border-radius: 0.75rem !important;
}

/* Smaller font for the complex directory tree */
.tree-code .shiki {
font-size: 0.65rem !important;
line-height: 1.1 !important;
border: 1px solid #e5e7eb !important;
background-color: #fcfcfc !important;
}
</style>

---
transition: slide-up
layout: default
---

# Energy Flows
<p class="opacity-50 -mt-4 mb-8 text-lg">System Level Sankey Charts</p>

<div class="grid grid-cols-[0.50fr_1.50fr] gap-10 h-[440px]">

  <div class="flex flex-col justify-top gap-10 h-full p-0 pt-10">
    <div class="custom-code">
```ts{1-4,5,9,10}
.
└── pypsa-usa/
  └── ...
      └── figures/
          └── system/
              ├── capacity
              ├── emissions
              ├── production
              ├── sankey/
              │   ├── energy.html
              │   └── carbon.html
              └── natural_gas
```
</div>

</div>

<div class="flex flex-col justify-center gap-0 -mt-35">
<div class="px-4 py-4 rounded-2xl">
<img src="/assets/s21/sankey.png" class="w-full object-contain rounded-xl max-h-[400px]" alt="Energy Flows" />
</div>
<div class="text-center text-[11px] opacity-40 uppercase tracking-widest mt-2">Energy Flows from PyPSA-USA</div>

</div>

</div>

<style>
.shiki {
font-size: 0.75rem !important;
line-height: 1 !important;
border: 1px solid #e5e7eb !important;
}
</style>

---
transition: slide-up
layout: two-cols
---

# Energy Flows
<p class="opacity-50 -mt-4 mb-8 text-lg">System Level Validation</p>

::left::

<div class="flex flex-col gap-4 justify-center h-full pr-2 -mt-10">
  <img src="/assets/s22/eia-sankey.png" class="w-full object-contain max-h-[300px]" alt="EIA Sankey" />
</div>

::right::

<div class="flex flex-col gap-4 justify-center h-full pl-2 mt-10">
  <img src="/assets/s22/lbln-sankey.png" class="w-full object-contain max-h-[300px]" alt="LBNL Sankey" />
</div>

---
transition: slide-up
layout: default
---

# Carbon Flows
<p class="opacity-50 -mt-4 mb-8 text-lg">System Level Sankey Charts</p>

<div class="grid grid-cols-[0.50fr_1.50fr] gap-10 h-[440px]">

  <div class="flex flex-col justify-top gap-10 h-full p-0 pt-10">
    <div class="custom-code">
```ts{1-4,5,9,11}
.
└── pypsa-usa/
  └── ...
      └── figures/
          └── system/
              ├── capacity
              ├── emissions
              ├── production
              ├── sankey/
              │   ├── energy.html
              │   └── carbon.html
              └── natural_gas
```
</div>

</div>

<div class="flex flex-col justify-center gap-0 -mt-35">
<div class="px-4 py-4 rounded-2xl">
<img src="/assets/s23/sankey.png" class="w-full object-contain rounded-xl max-h-[400px]" alt="Energy Flows" />
</div>
<div class="text-center text-[11px] opacity-40 uppercase tracking-widest mt-2">Carbon Flows from PyPSA-USA</div>

</div>

</div>

<style>
.shiki {
font-size: 0.75rem !important;
line-height: 1 !important;
border: 1px solid #e5e7eb !important;
}
</style>

---
transition: slide-up
layout: default
---

# Production
<p class="opacity-50 -mt-4 mb-8 text-lg">System Level Production Results</p>

<div class="grid grid-cols-[0.50fr_1.50fr] gap-10 h-[440px]">
  
  <div class="flex flex-col justify-top gap-10 h-full p-0 pt-10">
    <div class="custom-code">
```ts{1-5,8-12}
.
└── pypsa-usa/
  └── ...
      └── figures/
          └── system/
            ├── capacity
            ├── emissions
            ├── production/
            │   ├── pwr/
            │   │   └── production_time_series.png
            │   └── res/
            │       └── production_time_series.png
            ├── sankey
            └── natural_gas
```
</div>

</div>

<div class="flex flex-col h-full items-center gap-4 -mt-10">
<div class="w-full">
<img src="/assets/s24/pwr.png" class="w-full h-auto max-h-[200px] object-contain" alt="Power Time Series" />
</div>
<div class="w-full">
<img src="/assets/s24/res.png" class="w-full h-auto max-h-[200px] object-contain" alt="Residential Time Series" />
</div>
</div>

</div>

---
transition: slide-up
layout: default
---

# Capacity
<p class="opacity-50 -mt-4 mb-8 text-lg">System Level Capacity Results</p>

<div class="grid grid-cols-[0.50fr_1.50fr] gap-10 h-[440px]">
  
  <div class="flex flex-col justify-top gap-10 h-full p-0 pt-10">
    <div class="custom-code">
```ts{1-10}
.
└── pypsa-usa/
  └── ...
      └── figures/
          └── system/
              ├── capacity/
              │   ├── pwr/
              │   │   └── end_use_cap_brownfield.png
              │   └── res/
              │       └── end_use_cap_brownfield.png
              ├── emissions
              ├── production
              ├── sankey
              └── natural_gas
```
</div>

</div>

<div class="flex flex-col h-full justify-center items-center gap-4 -mt-15">
<div class="w-full">
<img src="/assets/s25/pwr.png" class="w-full h-auto max-h-[200px] object-contain" alt="Power Time Series" />
</div>
<div class="w-full">
<img src="/assets/s25/res.png" class="w-full h-auto max-h-[200px] object-contain" alt="Residential Time Series" />
</div>
</div>

</div>

---
transition: slide-up
layout: default
---

# Natural Gas
<p class="opacity-50 -mt-4 mb-8 text-lg">System Level Natural Gas Results</p>

<div class="grid grid-cols-[0.50fr_1.50fr] gap-10 h-[440px]">
  
  <div class="flex flex-col justify-top gap-10 h-full p-0 pt-10">
    <div class="custom-code">
```ts{1-5,10,11,12}
.
└── pypsa-usa/
  └── ...
      └── figures/
          └── system/
              ├── capacity
              ├── emissions
              ├── production
              ├── sankey
              └── natural_gas/
                  ├── demand.png
                  ├── domestic_trade.png
                  ├── international_trade.png
                  ├── fuel_price.png
                  ├── linepack.png
                  ├── processing.png
                  └── storage.png
```
</div>

</div>

<div class="flex flex-col h-full justify-center items-center gap-4 -mt-20">
<div class="w-full">
<img src="/assets/s26/demand.png" class="w-full h-auto max-h-[200px] object-contain" alt="Power Time Series" />
</div>
<div class="w-full">
<img src="/assets/s26/domestic_trade.png" class="w-full h-auto max-h-[200px] object-contain" alt="Residential Time Series" />
</div>
</div>

</div>


---
transition: slide-up
level: 2
---

# Conclusion
<!-- <p class="opacity-50 -mt-4 mb-10 text-lg">Evaluating regional decarbonization potential and system transition</p> -->
<div v-click>
  <h2 class="text-primary font-600 mb-4 border-b border-gray-10 pb-2">
    Research Question
  </h2>
  Evaluate regional decarbonization pathways for New England by 2030
</div>

<div class="grid grid-cols-2 gap-8 items-stretch p-6">

  <div v-click class="bg-gray-50 p-6 rounded-2xl border border-gray-10 shadow-sm flex flex-col justify-between">
    <h2 class="text-primary font-600 mb-6 border-b border-gray-10 pb-2 flex items-center gap-3">
      What did we do?
    </h2>
    <div class="space-y-5 flex-grow">
      <div class="flex items-start gap-4">
        <div class="text-xl">💻</div>
        <div>
          <div class="font-bold">PyPSA-USA Sector Setup</div>
          <div class="text-sm opacity-70">Enabled cross-sectoral energy analysis</div>
        </div>
      </div>
      <div class="flex items-start gap-4">
        <div class="text-xl">📜</div>
        <div>
          <div class="font-bold">Policy Evaluation</div>
          <div class="text-sm opacity-70">Implemented sector specific policies</div>
        </div>
      </div>
      <div class="flex items-start gap-4">
        <div class="text-xl">📊</div>
        <div>
          <div class="font-bold">Result Analysis</div>
          <div class="text-sm opacity-70">Viewed auto-generated charts</div>
        </div>
      </div>
    </div>
  </div>

  <div v-click class="bg-gray-50 p-6 rounded-2xl border border-gray-10 shadow-sm">
    <h2 class="text-primary font-600 mb-6 border-b border-gray-10 pb-2 flex items-center gap-3">
      Future Improvments
    </h2>
    <div class="space-y-6">
      <div class="flex items-center gap-4">
        <div class="text-2xl">⛽</div>
        <div>
          <div class="font-bold">Alternative fuels</div>
          <div class="text-sm opacity-70">Hydrogen, biofuels, etc. supply chains</div>
        </div>
      </div>
      <div class="flex items-center gap-4">
        <div class="text-2xl">🏭</div>
        <div>
          <div class="font-bold">Industrial Sector</div>
          <div class="text-sm opacity-70">Improvments on industrial demand and technology representation</div>
        </div>
      </div>
      <div class="flex items-center gap-4">
        <div class="text-2xl">✈️</div>
        <div>
          <div class="font-bold">Non-road vehicle transport</div>
          <div class="text-sm opacity-70">Air, train, and marine decarbonization</div>
        </div>
      </div>
    </div>
  </div>
</div>

---
layout: center
class: "text-center"
transition: slide-up
---

# Thank You! 

[GitHub](https://github.com/PyPSA/pypsa-usa/tree/master) / [Documentation](https://pypsa-usa.readthedocs.io/en/latest/)
