# STCO Co-Design Simulator v2 — Comprehensive QA Test Plan

**Target:** https://kvbulusu.github.io/ai-silicon-simulator/  
**Version:** v2 — 2026 Edition  
**Date:** 2026-07-15  
**Author:** QA Automation  
**Source Code:** `simulator_v2_comprehensive.html` (1482 lines)  
**Hardware Database:** `simulator_hardware_database_2026.json` (20 presets, 9 models)

---

## Table of Contents

1. [TC1: Hardware Preset Loading & Spec Accuracy](#tc1-hardware-preset-loading--spec-accuracy)
2. [TC2: Roofline Model Correctness](#tc2-roofline-model-correctness)
3. [TC3: Precision Scaling Impact](#tc3-precision-scaling-impact)
4. [TC4: Workload Type Switching](#tc4-workload-type-switching)
5. [TC5: AI Model Selection & Memory Fit Validation](#tc5-ai-model-selection--memory-fit-validation)
6. [TC6: TCO & Power Iceberg Calculations](#tc6-tco--power-iceberg-calculations)
7. [TC7: Build-vs-Buy & Software NRE Analysis](#tc7-build-vs-buy--software-nre-analysis)
8. [TC8: Agentic AI Economics & Workflow Visualization](#tc8-agentic-ai-economics--workflow-visualization)
9. [TC9: Book Scenario Presets](#tc9-book-scenario-presets)
10. [TC10: Configuration Warnings & Validation](#tc10-configuration-warnings--validation)
11. [TC11: Compare Mode](#tc11-compare-mode)
12. [TC12: Export, State Persistence & Edge Cases](#tc12-export-state-persistence--edge-cases)

---

## TC1: Hardware Preset Loading & Spec Accuracy

**Objective:** Verify every hardware preset loads correct specs from HW_DB and all dependent UI fields update without stale values.

### TC1.1 — NVIDIA H100 SXM5 Preset
- **Steps:** Select "H100 SXM5 (5nm, 700W)" from Hardware Preset dropdown.
- **Expected:**
  - Node dropdown → `5nm`
  - Packaging → `2.5D CoWoS`
  - Memory → `HBM3 (3350)`
  - Link → `NVLink4 (450)`
  - Precision → `FP8`
  - Cooling → `Liquid`
  - Clock slider → `1980` MHz
  - TDP slider → `700` W
  - Cores slider → `16896`
  - Mem Cap slider → `80` GB
  - Workload type auto-set → `Inference — Decode`

### TC1.2 — NVIDIA B200 Preset
- **Steps:** Select "B200 (4nm, 1000W, 192GB)".
- **Expected:**
  - Node → `4nm`, Pkg → `2.5D CoWoS`, Memory → `HBM3e (4800)`, Link → `NVLink5 (900)`
  - Precision → `FP4/MXFP4`, Cooling → `Liquid`
  - Clock → `2100`, TDP → `1000`, Cores → `20480`, MemCap → `192`

### TC1.3 — AMD MI300X Preset
- **Steps:** Select "MI300X (5nm, 750W)".
- **Expected:**
  - Node → `5nm`, Pkg → `3D Stack`, Memory → `HBM3 (3350)`, Link → `UALink (400)`
  - Precision → `FP8`, Cooling → `Liquid`
  - Clock → `1700`, TDP → `750`, Cores → `19456`, MemCap → `192`

### TC1.4 — AMD MI350 Preset
- **Steps:** Select "MI350 (3nm, 750W)".
- **Expected:**
  - Node → `3nm`, Pkg → `3D Stack`, Memory → `HBM3e (4800)`, Link → `UALink (400)`
  - Precision → `FP8`, Cooling → `Liquid`
  - Clock → `1900`, TDP → `750`, Cores → `20480`, MemCap → `288`

### TC1.5 — Intel Gaudi 3 Preset
- **Steps:** Select "Gaudi 3 (5nm, 600W)".
- **Expected:**
  - Node → `5nm`, Pkg → `2.5D CoWoS`, Memory → `HBM2e (2000)`, Link → `PCIe5 (64)`
  - Precision → `FP8`, Cooling → `Liquid`
  - Clock → `1500`, TDP → `600`, Cores → `8192`, MemCap → `128`

### TC1.6 — Edge AI: Jetson Orin NX Preset
- **Steps:** Select "Jetson Orin NX (25W)".
- **Expected:**
  - Node → `7nm`, Pkg → `Monolithic`, Memory → `LPDDR5 (100)`, Link → `PCIe5 (64)`
  - Precision → `INT8`, Cooling → `Air`
  - Clock → `918`, TDP → `25`, Cores → `1024`, MemCap → `16`
  - Workload type auto-set → `Edge Inference`

### TC1.7 — Edge AI: Google Edge TPU Preset
- **Steps:** Select "Google Edge TPU (4W)".
- **Expected:**
  - Node → `14nm`, Pkg → `Monolithic`, Memory → `DDR5 (80)`, Link → `USB (5)`
  - Precision → `INT8`, Cooling → `Passive`
  - Clock → `500`, TDP → `4`, Cores → `256`, MemCap → `2`
  - Workload type auto-set → `Edge Inference`

### TC1.8 — AI PC/NPU: Intel Core Ultra NPU Preset
- **Steps:** Select "Intel Core Ultra NPU".
- **Expected:**
  - Node → `7nm`, Pkg → `Monolithic`, Memory → `LPDDR5 (100)`, Link → `PCIe5 (64)`
  - Precision → `INT8`, Cooling → `Air`
  - Clock → `1400`, TDP → `28`, Cores → `512`, MemCap → `32`
  - Workload type auto-set → `AI PC / NPU`

### TC1.9 — AI PC/NPU: Apple M4 Neural Engine Preset
- **Steps:** Select "Apple M4 Neural Engine".
- **Expected:**
  - Node → `3nm`, Pkg → `Monolithic`, Memory → `LPDDR5 (100)`, Link → `PCIe5 (64)`
  - Precision → `FP16/BF16`, Cooling → `Passive`
  - Clock → `2000`, TDP → `22`, Cores → `384`, MemCap → `32`
  - Workload type auto-set → `AI PC / NPU`

### TC1.10 — Stale Value Check: Rapid Preset Switching
- **Steps:** Select H100 → immediately select Edge TPU → immediately select B200.
- **Expected:** All fields reflect B200 values. No stale H100 or Edge TPU values remain in any dropdown or slider.

### TC1.11 — NVIDIA A100 PCIe Preset
- **Steps:** Select "A100 PCIe (7nm, 400W)".
- **Expected:**
  - Node → `7nm`, Pkg → `Monolithic`, Memory → `HBM2e (2000)`, Link → `PCIe5 (64)`
  - Precision → `FP16/BF16`, Cooling → `Air`
  - Clock → `1410`, TDP → `400`, Cores → `6912`, MemCap → `80`

### TC1.12 — NVIDIA B100 Preset
- **Steps:** Select "B100 (4nm, 700W, 192GB)".
- **Expected:**
  - Node → `4nm`, Pkg → `2.5D CoWoS`, Memory → `HBM3e (4800)`, Link → `NVLink5 (900)`
  - Precision → `FP4/MXFP4`, Cooling → `Liquid`
  - Clock → `1800`, TDP → `700`, Cores → `18432`, MemCap → `192`

### TC1.13 — NVIDIA H200 Preset
- **Steps:** Select "H200 (5nm, 700W, 141GB)".
- **Expected:**
  - Node → `5nm`, Pkg → `2.5D CoWoS`, Memory → `HBM3e (4800)`, Link → `NVLink4 (450)`
  - Precision → `FP8`, Cooling → `Liquid`
  - Clock → `1980`, TDP → `700`, Cores → `16896`, MemCap → `141`

### TC1.14 — Custom Silicon Mode
- **Steps:** Select "🔧 Design Custom ASIC".
- **Expected:** All sliders remain editable. No preset values are loaded. Simulation still runs.

---

## TC2: Roofline Model Correctness

**Objective:** Verify the roofline chart correctly identifies memory-bound vs compute-bound regimes and the operating point moves correctly.

### TC2.1 — Memory-Bound Operating Point (Decode Workload)
- **Steps:** Select H100, Workload = "Inference — Decode", Compiler Fusion = 0%.
- **Expected:**
  - Arithmetic intensity = 0.12 (from LLaMA 3 70B model default)
  - effectiveIntensity = 0.12 × (1 + 0/100 × 3) = 0.12
  - memCeil = 0.12 × 3.35 = 0.402 TFLOPS
  - computeCeil = 16896 × 1980 × 0.0000296 × 4 (FP8) = 3963 TFLOPS
  - attained = min(0.402, 3963) = 0.402 TFLOPS → **Memory BW bottleneck**
  - Bottleneck indicator shows "Memory BW"
  - Operating point dot is in the memory-bound (left/yellow) region of roofline

### TC2.2 — Compute-Bound Operating Point (Training Workload)
- **Steps:** Select H100, Workload = "Training (Compute Heavy)", Compiler Fusion = 0%.
- **Expected:**
  - baseIntensity = 100 (training default, but model override applies if model selected)
  - If model = LLaMA 3 70B: intensity = 0.12 (model overrides workload!)
  - **BUG CHECK:** Training workload should use high intensity but model override may force low intensity
  - If custom model: effectiveIntensity = 100 × 1.0 = 100
  - memCeil = 100 × 3.35 = 335 TFLOPS
  - computeCeil ≈ 3963 TFLOPS
  - attained = 335 TFLOPS → Still memory-bound at FP8!
  - Operating point should be near the knee of the roofline

### TC2.3 — Prefill Workload (Compute-Bound)
- **Steps:** Select H100, Workload = "Inference — Prefill", Model = Custom, Compiler Fusion = 0%.
- **Expected:**
  - baseIntensity = 50 (prefill default)
  - effectiveIntensity = 50
  - memCeil = 50 × 3.35 = 167.5 TFLOPS
  - computeCeil ≈ 3963 TFLOPS
  - attained = 167.5 → Memory BW still bottleneck
  - **NOTE:** Even prefill is memory-bound at these intensities — verify this is intentional

### TC2.4 — Compiler Fusion Impact on Roofline
- **Steps:** H100, Decode, Fusion = 0% → note attained. Then Fusion = 100%.
- **Expected:**
  - At 0%: effectiveIntensity = baseIntensity × 1.0
  - At 100%: effectiveIntensity = baseIntensity × (1 + 1.0 × 3.0) = baseIntensity × 4.0
  - Attained TFLOPS should increase (operating point moves right on roofline)
  - memCeil = effectiveIntensity × memBWTBS increases 4×

### TC2.5 — Roofline Canvas Renders Without Errors
- **Steps:** Load simulator, switch to Performance tab.
- **Expected:**
  - Canvas renders without JS errors (check console)
  - X-axis label: "Arithmetic Intensity (FLOPs/Byte)"
  - Y-axis label: "Performance (TFLOPS)"
  - Legend shows Compute (purple), Memory (yellow), Network (teal)
  - Operating point dot is visible with crosshairs

---

## TC3: Precision Scaling Impact

**Objective:** Verify precision changes correctly scale throughput and propagate to all dependent calculations.

### TC3.1 — FP32 to FP16 Scaling on H100
- **Steps:** Select H100, set Precision = FP32. Note attained TFLOPS. Switch to FP16.
- **Expected:**
  - precTFLOPSMult: FP32=0.5, FP16=1.0 → 2× increase in peak TFLOPS
  - H100 FP32 peak: 16896 × 1980 × 0.0000296 × 0.5 = ~495 TFLOPS
  - H100 FP16 peak: 16896 × 1980 × 0.0000296 × 1.0 = ~990 TFLOPS
  - Token throughput should approximately double (if compute-bound)

### TC3.2 — FP16 to FP8 Scaling on H100
- **Steps:** H100, Precision FP16 → FP8.
- **Expected:**
  - precTFLOPSMult: FP16=1.0, FP8=2.0 → 2× increase
  - H100 FP8 peak: ~1979 TFLOPS
  - Decode token throughput changes based on precBytes (FP16=2, FP8=1)
  - decodeTokPerSecPerUser = memBW × 1e9 / (params × bytesPerParam)
  - FP8 bytesPerParam = 1 vs FP16 = 2 → 2× more tokens/s in decode

### TC3.3 — FP4 on Blackwell (B200) — Should Work
- **Steps:** Select B200 (which defaults to FP4). Verify calculations.
- **Expected:**
  - precTFLOPSMult for FP4 = 4.0
  - B200 FP4 peak: 20480 × 2100 × 0.0000296 × 4 = ~5094 TFLOPS
  - precBytes for FP4 = 0.5
  - No warning about FP4 compatibility (B200 is 4nm)

### TC3.4 — FP4 on Non-Blackwell Hardware (H100) — Should Warn
- **Steps:** Select H100 (5nm), manually change Precision to FP4.
- **Expected:**
  - Warning panel should show: "FP4/MXFP4 requires Blackwell-class (4nm+) hardware for native support."
  - **Source code check:** Warning triggers when `prec === 'fp4' && !['4nm','3nm','2nm'].includes(node)`
  - H100 is 5nm → warning SHOULD appear

### TC3.5 — INT8 and INT4 Scaling
- **Steps:** H100, switch between INT8 and INT4.
- **Expected:**
  - INT8: precMult=4, precBytes=1, precTFLOPSMult=2
  - INT4: precMult=8, precBytes=0.5, precTFLOPSMult=4
  - INT4 should give 2× throughput vs INT8

### TC3.6 — Precision Impact on Token Cost
- **Steps:** H100, FP16 → note cost/1K tokens. Switch to FP8.
- **Expected:**
  - Cost/1K tokens = (totalPower × elecRate / 3600000 / tokPerSec × 1000)
  - If tokPerSec doubles, cost/1K tokens should halve (power stays ~same)

---

## TC4: Workload Type Switching

**Objective:** Verify each workload type applies correct defaults and the UI responds appropriately.

### TC4.1 — Inference-Decode Defaults
- **Steps:** Select "Inference — Decode (Memory Bound)".
- **Expected:**
  - Description: "Memory-bound autoregressive decode. Batch serving, GPU ~90%."
  - baseIntensity = 0.15 (but model override may apply)
  - Bottleneck should be "Memory BW" for datacenter GPUs

### TC4.2 — Inference-Prefill Defaults
- **Steps:** Select "Inference — Prefill (Compute Bound)".
- **Expected:**
  - Description: "Compute-bound prompt processing. High FLOPS utilization."
  - baseIntensity = 50 (if custom model)
  - Token throughput uses prefillTokPerSec formula

### TC4.3 — Agentic AI Defaults & Tab Switch
- **Steps:** Select "Agentic AI (Multi-Step)".
- **Expected:**
  - Description: "Multi-step AI agent: planning→routing→tools→reasoning. GPU idle ~79% of time."
  - baseIntensity = 0.15
  - **Tab auto-switches to Agentic AI tab** (per source code line 464)
  - GPU utilization shows ~21% (calculated from phases)

### TC4.4 — Training Defaults
- **Steps:** Select "Training (Compute Heavy)".
- **Expected:**
  - Description: "Compute-heavy forward+backward passes. Large batches, high GPU util."
  - baseIntensity = 100 (if custom model)
  - Token throughput uses prefillTokPerSec formula (line 660: training uses prefill path)

### TC4.5 — Edge Inference Defaults
- **Steps:** Select "Edge Inference".
- **Expected:**
  - Description: "Power-constrained inference. Latency-critical, small batches."
  - baseIntensity = 0.3

### TC4.6 — AI PC / NPU Defaults
- **Steps:** Select "AI PC / NPU".
- **Expected:**
  - Description: "On-device NPU inference. Battery-aware, privacy-focused."
  - baseIntensity = 0.25

### TC4.7 — MoE Distributed Defaults
- **Steps:** Select "MoE Distributed (Network Bound)".
- **Expected:**
  - Description: "Mixture-of-Experts with cross-GPU routing. Network-bound."
  - baseIntensity = 0.5
  - commWeight = 0.75 (network becomes a factor)
  - Network ceiling line appears on roofline chart
  - Bottleneck may show "Network" depending on link BW

### TC4.8 — Workload Type Does NOT Reset Hardware Preset
- **Steps:** Select H100 preset. Then change workload to Training. Check hardware fields.
- **Expected:** All H100 hardware values remain (clock, TDP, cores, etc.). Only workload-related parameters change.

---

## TC5: AI Model Selection & Memory Fit Validation

**Objective:** Verify model presets configure correctly and memory fit warnings are accurate.

### TC5.1 — LLaMA 3 8B on H100 (Fits)
- **Steps:** Select H100 (80GB), Model = LLaMA 3 8B (16GB).
- **Expected:**
  - Model fit indicator: "✓ Model fits (16GB / 80GB)" in green
  - Batch size auto-set to 64
  - Arithmetic intensity overridden to 0.15

### TC5.2 — LLaMA 3 70B on H100 (Exceeds Memory)
- **Steps:** Select H100 (80GB), Model = LLaMA 3 70B (140GB).
- **Expected:**
  - Model fit indicator: "✗ Model too large (140GB > 80GB)" in red
  - Warning panel shows: "Model (140GB) exceeds memory capacity (80GB). Multi-GPU or quantize."
  - Batch size auto-set to 32

### TC5.3 — GPT-4 Scale on H100 (Massively Exceeds)
- **Steps:** Select H100 (80GB), Model = GPT-4 Scale (~1.8T MoE) (3600GB).
- **Expected:**
  - Model fit: "✗ Model too large (3600GB > 80GB)" in red
  - Critical warning about memory overflow
  - Batch size auto-set to 8

### TC5.4 — LLaMA 3 70B on B200 (Fits with 192GB)
- **Steps:** Select B200 (192GB), Model = LLaMA 3 70B (140GB).
- **Expected:**
  - Model fit: "✓ Model fits (140GB / 192GB)" in green

### TC5.5 — LLaMA 3 8B on Edge TPU (2GB — Exceeds)
- **Steps:** Select Edge TPU (2GB), Model = LLaMA 3 8B (16GB).
- **Expected:**
  - Model fit: "✗ Model too large (16GB > 2GB)" in red

### TC5.6 — Custom Model Selection
- **Steps:** Select "— Custom Parameters —" from model dropdown.
- **Expected:**
  - No batch size override occurs
  - modelMem = memCap × 0.8 (line 650: fallback for custom)
  - Model fit check uses this calculated value

### TC5.7 — Model Override of Arithmetic Intensity
- **Steps:** Select H100, Workload = Training (intensity=100), Model = LLaMA 3 70B.
- **Expected:**
  - baseIntensity = 0.12 (model overrides workload's 100!)
  - **POTENTIAL BUG:** Training workload with a specific model uses model's low intensity (0.12) instead of training's high intensity (100). This makes training appear memory-bound, which is incorrect for real training workloads.

---

## TC6: TCO & Power Iceberg Calculations

**Objective:** Verify all economic calculations are mathematically correct.

### TC6.1 — H100 Baseline TCO Calculation
- **Steps:** Select H100, Economics inputs: $/kWh=0.12, PUE=1.3, Years=3, GPU Count=8, default other values.
- **Expected (manual calculation):**
  - hwCost = $25,000 (from HW_DB)
  - hwCapex = 25000 × 8 = $200,000
  - infraCost = 200000 × 0.2 = $40,000
  - totalCapex = $240,000
  - chipPowerKW = (totalPower × 8) / 1000 (totalPower from thermal sim)
  - gridPowerKW = chipPowerKW × 1.3
  - annualPowerCost = gridPowerKW × 8760 × 0.12
  - totalPowerCost = annualPowerCost × 3
  - maintenanceCost = 240000 × 0.1 × 3 = $72,000
  - totalTCO = totalCapex + totalPowerCost + maintenanceCost
  - Verify displayed values match these calculations

### TC6.2 — Power Iceberg Cascade Accuracy
- **Steps:** H100 default config, check Economics → Power Iceberg panel.
- **Expected:**
  - Chip level: totalPower W
  - Server level: totalPower × (1 + 0.08) = totalPower × 1.08 (VRM +8%)
  - Rack level: serverW × (1 + 0.10) × gpuCount (PSU +10%)
  - Datacenter level: rackW × PUE (×1.3)
  - Total multiplier: (1.08) × (1.10) × 1.3 = 1.5444×
  - **BUG CHECK:** Source code line 977 shows `Rack (×${r.gpuCount})` as a template literal inside a regular string — this will render literally as `${r.gpuCount}` instead of the actual number!

### TC6.3 — Cloud Comparison (AWS p5.48xlarge)
- **Steps:** H100, 8 GPUs, 3 years.
- **Expected:**
  - Cloud hourly rate: $98.32/hr (hardcoded)
  - Cloud 3yr TCO: 98.32 × 8760 × 3 = $2,583,849.60
  - Savings = cloudTCO - totalTCO
  - Payback days = totalCapex / (98.32 × 24)
  - Verify all displayed values match

### TC6.4 — PUE Slider Impact
- **Steps:** Change PUE from 1.3 to 2.0. Check Power Iceberg and TCO.
- **Expected:**
  - Datacenter power increases proportionally
  - Total multiplier increases
  - Annual grid cost increases
  - Total TCO increases

### TC6.5 — Electricity Rate Impact
- **Steps:** Change $/kWh from 0.12 to 0.25.
- **Expected:**
  - Annual power cost roughly doubles
  - Total TCO increases
  - Cost/1K tokens increases

### TC6.6 — GPU Count Impact on TCO
- **Steps:** Change GPU Count from 8 to 64.
- **Expected:**
  - CapEx scales linearly (8× increase)
  - Power cost scales linearly
  - Maintenance scales linearly

---

## TC7: Build-vs-Buy & Software NRE Analysis

**Objective:** Verify custom silicon economics and recommendation logic.

### TC7.1 — NRE Calculation Accuracy
- **Steps:** H100 preset, Eng Cost = $180K.
- **Expected:**
  - swNRE = 40 × 180000 × 3 = $21,600,000
  - siliconNRE = $45,000,000
  - tapeoutCost = $20,000,000
  - totalNRE = 21,600,000 + 45,000,000 + 20,000,000 = $86,600,000
  - unitCost = $482 (hardcoded)
  - breakEvenUnits = ceil(86,600,000 / (25000 - 482)) = ceil(86,600,000 / 24,518) = 3,532 units

### TC7.2 — BUY Recommendation (Low Volume)
- **Steps:** Set Prod Volume = 1 (default).
- **Expected:**
  - Recommendation: "✅ BUY" (volume < 50,000)
  - Message mentions volume too low for NRE amortization

### TC7.3 — EVALUATE Recommendation (Medium Volume)
- **Steps:** Set Prod Volume = 100,000.
- **Expected:**
  - Recommendation: "⚠️ EVALUATE CAREFULLY" (50,000 ≤ volume < 500,000)

### TC7.4 — BUILD Recommendation (High Volume)
- **Steps:** Set Prod Volume = 1,000,000.
- **Expected:**
  - Recommendation: "✅ BUILD" (volume ≥ 500,000)
  - Per-unit savings displayed: $25,000 - $482 = $24,518

### TC7.5 — Software Maturity Levels Cost Calculation
- **Steps:** Eng Cost = $180K. Check Software Maturity panel.
- **Expected (per level):**
  - L1: 4 eng × $180K × (6/12) = $360,000
  - L2: 6 eng × $180K × (12/12) = $1,080,000
  - L3: 8 eng × $180K × (24/12) = $2,880,000
  - L4: 12 eng × $180K × (36/12) = $6,480,000
  - L5: 50 eng × $180K × (120/12) = $90,000,000

### TC7.6 — Engineering Cost Change Propagation
- **Steps:** Change Eng Cost from $180K to $250K. Check NRE and SW maturity costs.
- **Expected:**
  - swNRE = 40 × 250000 × 3 = $30,000,000
  - totalNRE = 30M + 45M + 20M = $95,000,000
  - All SW maturity level costs update proportionally

### TC7.7 — Break-Even with Different Hardware Costs
- **Steps:** Select A100 ($10,000) vs B200 ($40,000). Compare break-even units.
- **Expected:**
  - A100: breakEven = ceil(totalNRE / (10000 - 482)) = higher units needed
  - B200: breakEven = ceil(totalNRE / (40000 - 482)) = fewer units needed
  - More expensive hardware → lower break-even volume for custom silicon

---

## TC8: Agentic AI Economics & Workflow Visualization

**Objective:** Verify agentic AI workflow phases, GPU utilization, and economics comparison.

### TC8.1 — Workflow Phase Rendering
- **Steps:** Select Agentic AI workload, go to Agentic AI tab.
- **Expected:**
  - 5 phases rendered with timing bars:
    1. Orchestration: 2.5s, CPU:85%, GPU:5%
    2. Router LLM: 0.3s, CPU:20%, GPU:60%
    3. Tool Execution: 3.2s, CPU:70%, GPU:0%
    4. Reasoning: 0.8s, CPU:15%, GPU:90%
    5. Synthesis: 0.4s, CPU:10%, GPU:88%
  - Total: 7.2s
  - Bar widths proportional to duration

### TC8.2 — GPU Utilization Calculation
- **Steps:** Check GPU Active/Idle metrics.
- **Expected:**
  - GPU active phases (>30% GPU): Router LLM (0.3s), Reasoning (0.8s), Synthesis (0.4s) = 1.5s
  - gpuUtilAgentic = (1.5 / 7.2) × 100 = 20.83% ≈ 21%
  - GPU Idle = 79%
  - Queries/hr = 3600 / 7.2 = 500

### TC8.3 — Traditional vs Agentic Comparison Table
- **Steps:** Check the comparison table on Agentic AI tab.
- **Expected:**
  - Traditional queries/GPU/hr: 3600 / 1.2 = 3000
  - Agentic queries/GPU/hr: 500
  - Traditional GPU util: 90% (hardcoded display)
  - Agentic GPU util: 21%
  - Traditional CPU util: 8% (hardcoded display)
  - Agentic CPU util: 79% (hardcoded display)
  - Traditional latency: 1.2s
  - Agentic latency: 7.2s
  - Cost/query calculations use totalPower and elecRate

### TC8.4 — Resource Utilization Timeline (ASCII)
- **Steps:** Check Resource Utilization Timeline panel.
- **Expected:**
  - CPU bar: mostly █ (active) during Orchestration and Tool Execution
  - GPU bar: mostly ░ (idle) with brief █ during Router/Reasoning/Synthesis
  - NET bar: █ during Tool Execution
  - 20 time slots rendered
  - Total time shown as 7.2s

### TC8.5 — Agentic Phases Are Hardcoded (Not Hardware-Dependent)
- **Steps:** Switch hardware from H100 to Edge TPU while on Agentic workload.
- **Expected:**
  - Phase durations remain identical (2.5, 0.3, 3.2, 0.8, 0.4)
  - GPU utilization remains ~21%
  - **POTENTIAL ISSUE:** Agentic workflow timing doesn't scale with hardware capability — same latency on Edge TPU as H100

---

## TC9: Book Scenario Presets

**Objective:** Verify each book scenario loads correct configuration and navigates to the right tab.

### TC9.1 — Ch.8: H100 Cluster Power Analysis
- **Steps:** Select "Ch.8: H100 Cluster Power Analysis" from Book Scenarios.
- **Expected:**
  - Hardware preset → H100
  - Workload → Inference-Decode
  - Description text appears explaining Chapter 8 analysis
  - All H100 specs loaded correctly
  - Tab stays on current (or switches to Analysis per code logic)

### TC9.2 — Ch.8: DVFS Power-Performance Tradeoff
- **Steps:** Select "Ch.8: DVFS Power-Performance Tradeoff".
- **Expected:**
  - Hardware preset → H100
  - Workload → Inference-Decode
  - Clock frequency set to 2000 MHz (overridden by case study)
  - Description mentions changing clock from 2000→1200 MHz

### TC9.3 — Ch.10: HBM3 vs HBM3e vs HBM4
- **Steps:** Select "Ch.10: HBM3 vs HBM3e vs HBM4".
- **Expected:**
  - Hardware preset → H100 (with HBM3 default)
  - Workload → Inference-Decode
  - Description mentions switching memory types

### TC9.4 — Ch.11: Memory vs Compute Bottleneck
- **Steps:** Select "Ch.11: Memory vs Compute Bottleneck".
- **Expected:**
  - Hardware preset → H100
  - Workload → Inference-Decode
  - **Tab switches to Analysis** (code line 502: `cs.includes('bottleneck')`)
  - Description mentions switching between prefill and decode

### TC9.5 — Ch.14: Agentic vs Traditional Inference
- **Steps:** Select "Ch.14: Agentic vs Traditional Inference".
- **Expected:**
  - Hardware preset → H100
  - Workload → Agentic
  - **Tab switches to Agentic AI** (code line 500)
  - GPU utilization shows ~21%

### TC9.6 — Ch.16: Custom Silicon Build vs Buy
- **Steps:** Select "Ch.16: Custom Silicon Build vs Buy".
- **Expected:**
  - Hardware preset → H100
  - Workload → Inference-Decode
  - **Tab switches to Economics** (code line 501: `cs.includes('buildvbuy')`)
  - Build vs Buy panel visible

### TC9.7 — Exercise 8.1: Explore DVFS Tradeoff
- **Steps:** Select "Ex 8.1: Explore DVFS Tradeoff".
- **Expected:**
  - Hardware preset → H100
  - Clock frequency set to 800 MHz (overridden)
  - Description mentions sliding from 800→2200 MHz

### TC9.8 — Exercise 8.2: Power Iceberg
- **Steps:** Select "Ex 8.2: Power Iceberg for Your Facility".
- **Expected:**
  - Hardware preset → H100
  - **Tab switches to Economics** (code line 501: `cs.includes('iceberg')`)
  - Power Iceberg panel visible

### TC9.9 — Exercise 10.2: HBM vs DDR Cost-Performance
- **Steps:** Select "Ex 10.2: HBM vs DDR Cost-Performance".
- **Expected:**
  - Hardware preset → A100 (not H100!)
  - **Tab switches to Economics** (code line 501: `cs.includes('hbmcost')`)

### TC9.10 — Exercise 11.1: Determine Your Bottleneck
- **Steps:** Select "Ex 11.1: Determine Your Bottleneck".
- **Expected:**
  - Hardware preset → H100
  - **Tab switches to Analysis** (code line 502: `cs.includes('workload')`)

### TC9.11 — Exercise 11.2: Agentic vs Traditional Comparison
- **Steps:** Select "Ex 11.2: Agentic vs Traditional Comparison".
- **Expected:**
  - Hardware preset → H100
  - Workload → Agentic
  - **Tab switches to Agentic AI** (code line 500)

### TC9.12 — Scenario Description Clears on Deselect
- **Steps:** Select a scenario, then select "— Select Scenario —".
- **Expected:**
  - Description text clears (empty string)
  - No error in console

---

## TC10: Configuration Warnings & Validation

**Objective:** Verify all warning conditions trigger correctly and boundary values are handled.

### TC10.1 — Thermal Throttle Warning
- **Steps:** Select H100, set Cooling = Air, TDP = 700W, Clock = 2500 MHz.
- **Expected:**
  - Thermal solver iterates and reduces clock
  - Header shows "THROTTLE" in red
  - Bottleneck includes "⚠️ THROTTLE"
  - Warning: "TDP (XXW) exceeds limit (700W) → Throttling to YYY MHz"
  - Silicon diagram shows red overlay with "⚠️ THERMAL THROTTLE"

### TC10.2 — Power Throttle Warning
- **Steps:** Set very high cores (32768) with high clock (2500 MHz) and low TDP (200W).
- **Expected:**
  - Power exceeds TDP limit
  - Clock throttled down
  - Warning about power limit

### TC10.3 — Die Size Warning (>800mm²)
- **Steps:** Set Cores = 16896, Node = 5nm.
- **Expected:**
  - dieSize = 16896 × 0.05 = 844.8mm²
  - Warning: "Die size ~845mm² exceeds reticle limit. Consider chiplets."

### TC10.4 — Die Size Critical (>1000mm²)
- **Steps:** Set Cores = 20480, Node = 5nm.
- **Expected:**
  - dieSize = 20480 × 0.05 = 1024mm²
  - Critical warning: "Die size ~1024mm² too large for single die. Must use chiplet architecture."

### TC10.5 — Passive Cooling with High TDP
- **Steps:** Set Cooling = Passive, TDP = 700W.
- **Expected:**
  - Warning: "Passive cooling insufficient for 700W. Max recommended: 25W."

### TC10.6 — Memory Underutilization Info
- **Steps:** Set up compute-bound scenario (high intensity, low memory BW usage).
- **Expected:**
  - If memUtil < 20 and computeUtil > 80: Info message about memory BW underutilized

### TC10.7 — All Green (No Warnings)
- **Steps:** Select H100 with default settings (liquid cooling, 700W, 16896 cores).
- **Expected:**
  - Warning panel shows: "🟢 All parameters within normal ranges."

### TC10.8 — Slider Minimum Values
- **Steps:** Set Clock = 200 MHz (min), TDP = 2W (min), Cores = 64 (min), MemCap = 1 GB (min), Batch = 1 (min).
- **Expected:**
  - Simulation runs without errors
  - All values display correctly
  - No NaN or Infinity in outputs

### TC10.9 — Slider Maximum Values
- **Steps:** Set Clock = 2500 MHz (max), TDP = 1200W (max), Cores = 32768 (max), MemCap = 512 GB (max), Batch = 512 (max).
- **Expected:**
  - Simulation runs without errors
  - All values display correctly
  - Thermal throttling may occur but no crash

### TC10.10 — 3D Packaging Thermal Multiplier
- **Steps:** Select 3D Stack packaging with high TDP.
- **Expected:**
  - thermMult = 1.9 (vs 1.0 for monolithic)
  - Higher junction temperature
  - Insight bar mentions "3D stacking traps heat (1.9× thermal resistance)" if throttling

---

## TC11: Compare Mode

**Objective:** Verify side-by-side comparison works correctly with multiple configurations.

### TC11.1 — Add First Configuration
- **Steps:** Select H100, click "⚖️ Compare" button.
- **Expected:**
  - Tab switches to Compare
  - Table shows 1 column with H100 data
  - Label: "NVIDIA H100 SXM5 #1"
  - All fields populated (Node, TDP, Memory, Peak TFLOPS, Attained, Tokens/s, etc.)

### TC11.2 — Add Second Configuration
- **Steps:** Switch to B200, click "⚖️ Compare" again.
- **Expected:**
  - Table shows 2 columns: H100 #1 and B200 #2
  - Delta highlighting: green ✓ on better values
  - B200 should win on: Peak TFLOPS, Attained TFLOPS, Tokens/s, Memory
  - H100 should win on: Power (lower), Temp (lower), TCO (lower)

### TC11.3 — Add Third Configuration (Max)
- **Steps:** Switch to MI300X, click "⚖️ Compare".
- **Expected:**
  - Table shows 3 columns
  - Best value in each row highlighted green with ✓

### TC11.4 — Fourth Configuration Replaces Oldest
- **Steps:** Click "⚖️ Compare" again with a different config.
- **Expected:**
  - comparisonSlots.shift() removes the first entry
  - Table still shows 3 columns (max)
  - First column is now the second original config

### TC11.5 — Clear All Button
- **Steps:** Click "Clear All" in comparison panel.
- **Expected:**
  - All comparison data cleared
  - Panel shows empty state: "Click 'Compare' to add configs (max 3)."

### TC11.6 — Custom Config in Comparison
- **Steps:** Select "— Custom —" hardware, adjust sliders, click Compare.
- **Expected:**
  - Label shows "Custom Config #N" (since HW_DB lookup fails for empty preset)
  - **BUG CHECK:** `val('sel-preset')` returns empty string → `HW_DB['']` is undefined → label = "Custom Config"
  - hwCost falls back to $4,200 (line 672)

### TC11.7 — Comparison Table Field Accuracy
- **Steps:** Add H100 to comparison. Verify each field matches the main dashboard.
- **Expected:**
  - Node matches sel-node value
  - TDP matches sld-tdp value + "W"
  - Memory matches memCap + "GB " + memType
  - Peak TFLOPS = finalTFLOPS.toFixed(0)
  - Attained TFLOPS = attained.toFixed(0)
  - Tokens/s = formatNum(tokPerSec)
  - Latency/tok = latencyPerTok.toFixed(1) + "ms"
  - Power = totalPower.toFixed(0) + "W"
  - Temp = jTemp.toFixed(0) + "°C"
  - TCO = "$" + formatNum(totalTCO)
  - Bottleneck = bottleneck string

---

## TC12: Export, State Persistence & Edge Cases

**Objective:** Test export functionality, page refresh behavior, and edge cases.

### TC12.1 — Export JSON
- **Steps:** Configure H100, click "📥 Export" button.
- **Expected:**
  - Browser downloads file named "stco-config-v2.json"
  - File contains valid JSON with all simResult fields
  - Key fields present: node, pkg, freq, tdpLimit, cores, attained, bottleneck, totalTCO, etc.

### TC12.2 — Screenshot Capture
- **Steps:** Click "📷" button.
- **Expected:**
  - html2canvas captures the page
  - Browser downloads "stco-simulator-v2.png"
  - Image is readable and contains the full simulator UI

### TC12.3 — Page Refresh Resets State
- **Steps:** Configure B200 with custom settings. Refresh the page.
- **Expected:**
  - Welcome overlay appears again
  - All settings reset to defaults (no localStorage persistence)
  - This is expected behavior (no state persistence implemented)

### TC12.4 — Rapid Slider Changes (Race Condition)
- **Steps:** Rapidly drag the Clock slider back and forth 10+ times quickly.
- **Expected:**
  - No JS errors in console
  - Final displayed value matches slider position
  - All dependent calculations update to final value
  - No visual glitches in roofline or silicon diagrams

### TC12.5 — Rapid Preset Switching
- **Steps:** Quickly cycle through all presets: H100 → B200 → MI300X → Edge TPU → Apple M4 → H100.
- **Expected:**
  - Final state reflects H100 values
  - No stale values from intermediate presets
  - No console errors

### TC12.6 — Economics Inputs: Negative Values
- **Steps:** Enter -1 for $/kWh, -5 for PUE, 0 for Years.
- **Expected:**
  - Input fields have `min` attributes ($/kWh min=0, PUE min=1, Years min=1)
  - Browser should prevent negative values via HTML validation
  - If bypassed: calculations should not produce NaN or crash

### TC12.7 — Economics Inputs: Extreme Values
- **Steps:** Set GPU Count = 1024 (max), Years = 10 (max), $/kWh = 1.00.
- **Expected:**
  - TCO calculation produces very large but valid number
  - formatNum handles large values (B for billions)
  - No overflow or display issues

### TC12.8 — Collapsible Economics Panel
- **Steps:** Click "Economics Inputs" panel header to expand. Click again to collapse.
- **Expected:**
  - Panel expands showing $/kWh, PUE, Years, GPU Count, Prod Volume, Eng Cost fields
  - Arrow icon toggles between expand_more and expand_less
  - Panel collapses smoothly

### TC12.9 — Optimize For Toggle (Throughput vs Latency)
- **Steps:** Click "⏱️ Latency" button, then "⚡ Throughput" button.
- **Expected:**
  - Active button gets purple highlight (class 'ac')
  - optMode variable changes
  - runSim() is called on each toggle
  - **NOTE:** optMode is stored but never actually used in calculations (not referenced in runSim). This may be a feature gap.

### TC12.10 — Browser Console Errors Check
- **Steps:** Open browser console, load simulator, interact with all tabs and presets.
- **Expected:**
  - Zero JavaScript errors
  - No uncaught exceptions
  - No failed network requests (CDN resources load correctly)

### TC12.11 — Template Literal Bug in Power Iceberg
- **Steps:** Check Power Iceberg panel, look at the Rack level label.
- **Expected:**
  - **SUSPECTED BUG:** Line 977 in source: `{name:'Rack (×${r.gpuCount})',...}` — this is inside a regular object literal, NOT a template literal (the outer string uses single quotes). The `${r.gpuCount}` will render literally as the string "${r.gpuCount}" instead of the actual GPU count number.
  - Verify whether the Rack label shows "Rack (×8)" or "Rack (×${r.gpuCount})"

### TC12.12 — Template Literal Bug in Agentic Flow
- **Steps:** Check Agentic AI tab, look at the "Query Flow Timeline" header.
- **Expected:**
  - **SUSPECTED BUG:** Line 1052: `'<div ...><b>Query Flow Timeline (${r.agenticTotal.toFixed(1)}s total)</b></div>'` — uses single quotes, not backticks. The `${r.agenticTotal.toFixed(1)}` will render literally.
  - Verify whether it shows "Query Flow Timeline (7.2s total)" or the raw template string.

---

## Appendix A: Hardware Database Reference

| Preset | Node | TDP | MemType | MemBW | MemCap | Cores | Freq | Cost | Category |
|--------|------|-----|---------|-------|--------|-------|------|------|----------|
| H100 | 5nm | 700W | HBM3 | 3350 | 80GB | 16896 | 1980 | $25K | DC |
| H200 | 5nm | 700W | HBM3e | 4800 | 141GB | 16896 | 1980 | $30K | DC |
| B100 | 4nm | 700W | HBM3e | 8000 | 192GB | 18432 | 1800 | $35K | DC |
| B200 | 4nm | 1000W | HBM3e | 8000 | 192GB | 20480 | 2100 | $40K | DC |
| A100 | 7nm | 400W | HBM2e | 2000 | 80GB | 6912 | 1410 | $10K | DC |
| MI300X | 5nm | 750W | HBM3 | 5300 | 192GB | 19456 | 1700 | $22K | DC |
| MI350 | 3nm | 750W | HBM3e | 6000 | 288GB | 20480 | 1900 | $28K | DC |
| Gaudi 3 | 5nm | 600W | HBM2e | 3700 | 128GB | 8192 | 1500 | $15K | DC |
| Orin NX | 7nm | 25W | LPDDR5 | 100 | 16GB | 1024 | 918 | $500 | Edge |
| AGX Orin | 7nm | 60W | LPDDR5 | 205 | 64GB | 2048 | 1300 | $1.2K | Edge |
| Cloud AI 100 | 7nm | 75W | DDR5 | 134 | 32GB | 4096 | 1400 | $800 | Edge |
| Edge TPU | 14nm | 4W | DDR5 | 8 | 2GB | 256 | 500 | $75 | Edge |
| Core Ultra | 7nm | 28W | LPDDR5 | 68 | 32GB | 512 | 1400 | $400 | AIPC |
| Ryzen AI | 4nm | 28W | LPDDR5 | 68 | 32GB | 384 | 1600 | $350 | AIPC |
| Snapdragon X | 4nm | 23W | LPDDR5 | 68 | 32GB | 512 | 1800 | $500 | AIPC |
| Apple M4 | 3nm | 22W | LPDDR5 | 120 | 32GB | 384 | 2000 | $600 | AIPC |

## Appendix B: Key Formulas

```
calibFactor = 0.0000296 TFLOPS per (core × MHz) at FP16
rawPeakTFLOPS = cores × freq × calibFactor × precTFLOPSMult[prec]
effectiveIntensity = baseIntensity × (1 + fusion/100 × 3.0)
memCeil = effectiveIntensity × (memBW / 1000)
attained = min(computeCeil, memCeil, netCeil)
decodeTokPerSecPerUser = memBW × 1e9 / (modelParams × bytesPerParam)
decodeTokPerSec = decodeTokPerSecPerUser × min(batch, 128)
totalTCO = totalCapex + totalPowerCost + maintenanceCost
chipToGrid = (1 + vrmLoss) × (1 + psuLoss) × PUE
breakEvenUnits = ceil(totalNRE / (hwCost - unitCost))
```

## Appendix C: Suspected Bugs (Pre-Test)

1. **Template literal in single-quoted string (Power Iceberg):** Line 977 — `${r.gpuCount}` inside single quotes won't interpolate.
2. **Template literal in single-quoted string (Agentic Flow):** Line 1052 — `${r.agenticTotal.toFixed(1)}` inside single quotes won't interpolate.
3. **Model overrides workload intensity:** Line 590 — When a model is selected, its intensity overrides the workload type's intensity. Training workload with LLaMA 3 70B uses intensity 0.12 instead of 100, making training appear memory-bound.
4. **Agentic phases are hardware-independent:** Phase durations are hardcoded and don't scale with hardware capability.
5. **optMode (Throughput/Latency) is unused:** The toggle sets the variable but `runSim()` never references it.
6. **Cloud comparison uses single instance pricing:** $98.32/hr for p5.48xlarge compared against multi-GPU on-prem — may not be apples-to-apples.
7. **Decode throughput capped at batch 128:** Line 659 — `Math.min(batch, 128)` silently caps batch effect.

---

*Total sub-test-cases: 82*  
*Estimated execution time: 3-4 hours*
