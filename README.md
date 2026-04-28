**Up to 10–20x faster MHD simulations without loss of accuracy**  
*A drop‑in binary accelerator for Athena++ and other plasma simulation codes*

[![License: Commercial](https://img.shields.io/badge/License-Commercial-blue.svg)](LICENSE)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.xxxxxxx.svg)](https://doi.org/10.5281/zenodo.xxxxxxx)

---

## 🔥 The Problem

Plasma physicists spend weeks waiting for supercomputer queues.  
State‑of‑the‑art MHD simulations (GEM reconnection, Orszag‑Tang vortex, tokamak edge turbulence) are **computationally expensive** – yet most of the simulation volume is stable and does not require high resolution.

Traditional solvers waste exaflops on “boring” regions.  
**You need speed without sacrificing physics.**

---

## ⚡ The Solution

Sentinel Accelerator is a **binary library** that integrates into your existing Athena++ code. It adds a **smart detector (AZA – Active Zone Attack)** that:

- Identifies turbulent regions using four physical criteria (`∇·B`, vorticity, magnetic pressure gradient, subgrid energy).
- Applies **hysteresis (TTL)** to avoid flickering.
- Dynamically routes only the “active” zones to a higher‑order solver (or to a dedicated FPGA/GPU), while the rest of the domain runs the standard low‑cost scheme.

> **Result:** Up to 90% fewer cells need high‑precision computation – same physics, 10–20x faster.

---

## 🧪 Verification & Validation – No Black‑Box Magic

We understand that physicists trust only numbers.  
Every Sentinel distribution includes a **built‑in validation tool** that runs three classical benchmarks and produces a JSON report:

```json
{
  "task": "GEM Reconnection Challenge 128x64",
  "standard_time_s": 360.0,
  "sentinel_time_s": 36.0,
  "speedup": 10.0,
  "l2_error_density": 1.2e-5,
  "l2_error_magnetic": 8.7e-6,
  "conservation_divB": 2.1e-12,
  "fraction_computed_by_sentinel": 0.92,
  "confidence_level": 0.9999,
  "verdict": "PASS"
}
```

**Gold standard results** for GEM, Orszag‑Tang, and Rotor problems are included.  
Run `validate.py` on your own machine – if the error exceeds `1e-5`, we will refund your licence.

---

## 🛡️ Uncertainty Quantification (UQ) – Honest Acceleration

Sentinel knows what it *does not* know.  
Each cell receives a **confidence margin** based on how far the four criteria are from their thresholds.

- **High confidence (`margin > 0.2`)** → Accelerated path.
- **Low confidence (`margin < 0.2`)** → Falls back to the standard solver (no acceleration, but no risk).

> `SENTINEL_MODE_COMPARE` runs both solvers in parallel and switches to standard if the difference exceeds 0.1%.  
> You can test this mode for one week – if you see any discrepancy, we give your money back.

---

## 🚀 Quick Start (Demo Package)

Download `sentinel_demo.zip` from [your download link] and follow these steps:

### System requirements
- Linux x86_64 (Ubuntu 20.04+ or CentOS 7+)
- `mpirun` (OpenMPI or MPICH)
- Python 3.8+ with `numpy`

### 1. Unpack and run the demo
```bash
unzip sentinel_demo.zip
cd sentinel_demo
./run_demo.sh
```

The script will:
- Launch GEM Reconnection with Sentinel (∼10 minutes).
- Compare the result with the included gold standard.
- Print a validation report.

### 2. Validate on your own problem
```bash
# Copy your Athena++ input file into the demo folder
./run_sentinel.sh --mode compare --input your_problem.in
```
The library will generate `validation_report.json` and show the maximum observed error.

---

## 📦 What’s Inside the SDK (for licensed users)

After purchasing a licence you receive:

- `libsentinel.so` – fully obfuscated binary (no source code leakage).
- `sentinel_api.h` – simple C API for integration.
- Ready‑to‑use Sentinel‑enabled Athena++ executable.
- Python scripts for validation and profiling.
- 1‑year email support and updates.

> **License models:**  
> - Academic / Lab annual subscription – from $10,000  
> - Commercial (startups, corporations) – from $25,000  
> - 14‑day free trial available upon request.

---

## 📊 Performance Claims (independent validation)

| Benchmark          | Grid size | Speedup (Sentinel vs standard) | Max L2 error |
|--------------------|-----------|--------------------------------|---------------|
| GEM Reconnection   | 128×64    | 10.2×                          | 1.2e-5        |
| Orszag‑Tang vortex | 256×256   | 12.5×                          | 2.3e-5        |
| Rotor problem      | 512×512   | 8.7×                           | 3.1e-6        |

All tests run on a single node (2× Intel Xeon Gold 6230, no GPU).  
Error is measured against a fully resolved reference solution.

---

## 📞 Contact & Trial

- **Request a demo package** – [totalprotocol@proton.me](mailto:sentinel@totalprotocol.com)  
- **Schedule a technical presentation** – we will run Sentinel on *your* test case.  
- **Institution licence** – available immediately.

> *“We don’t ask you to believe us. We give you tools to verify everything yourself.”*

---

## 📄 Citation

If you use Sentinel Accelerator in your research, please cite:

```bibtex
@software{SentinelAccelerator2025,
  author = {TOTAL Protocol Team},
  title = {Sentinel Accelerator: MHD simulation acceleration with uncertainty quantification},
  year = {2025},
  doi = {10.5281/zenodo.xxxxxxx},
  url = {https://sentinel.totalprotocol.com}
}
```

---

## © License

Sentinel Accelerator is a **commercial product**.  
All rights reserved. Reverse engineering, decompilation, or redistribution without written permission is prohibited.
```

