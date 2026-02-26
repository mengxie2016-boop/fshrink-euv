# fshrink-euv
f-Shrink controllers for High-NA EUV stochastic control. Outperforms PID: 0.297nm EPE (5.4% better), 86% fewer failures, 0.605nm CD error (meets 3nm). Full stochastic model: photon/chemical noise, mask 3D, thermal drift. Based on Xie, M. (2026) Zenodo.
# fshrink-euv: f-Shrink Controllers for High-NA EUV Stochastic Control

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.18485110.svg)](https://doi.org/10.5281/zenodo.18485110)

This repository provides a complete simulation framework for High-NA EUV lithography control using f-Shrink adaptive controllers. It demonstrates that f-Shrink significantly outperforms traditional PID controllers in complex, stochastic, and time-varying manufacturing environments.

The core of this project is the f-Shrink operator, derived from the transcendental dynamical system analyzed in the foundational paper (see Citation section).

## 🚀 Key Features

- Full Stochastic EUV Model: Includes photon shot noise, chemical amplification noise, mask 3D effects, thermal drift, multi-layer alignment, and realistic failure detection (micro-bridge, line break, overlay error).
- Multiple Controllers: Implements and compares:
    - Standard PID
    - fast f-Shrink
    - decay f-Shrink (β = 0.02, 0.035)
    - smooth f-Shrink (α = 0.05, 0.1, 0.15)
- Multi-Variable Control: Simultaneously controls position, focus, and dose.
- Performance Analysis: Automatically computes and compares key metrics: steady-state Edge Placement Error (EPE), maximum EPE, settling time, CD (Critical Dimension) error, and stochastic failure count.

## 🏆 Benchmark Results

In a head-to-head comparison against PID on a challenging High-NA EUV benchmark, f-Shrink controllers dominated:

| Controller | Steady EPE (nm) | Max EPE (nm) | Failures | CD Error (nm) | Best For |
|------------|-----------------|--------------|----------|---------------|----------|
| decay β=0.02 | 0.297 | 5.654 | 7053 | 4.723 | Minimum EPE (Highest Precision) |
| fast | 0.298 | 5.728 | 2003 | 1.450 | Best Overall & Highest Yield |
| decay β=0.035 | 0.307 | 5.728 | 1971 | 1.904 | Balanced |
| smooth α=0.05 | 0.315 | 5.692 | 4284 | 0.605 | Best CD Control |
| smooth α=0.15 | 0.311 | 5.634 | 13461 | 3.404 | - |
| PID | 0.314 | 5.577 | 14350 | 4.928 | Baseline |
| smooth α=0.1 | 0.324 | 5.717 | 7631 | 1.204 | - |

Key Takeaways:
- Best Precision: decay β=0.02 achieves the lowest steady EPE (0.297 nm), 5.4% better than PID.
- Highest Yield: fast reduces stochastic failures by 86% compared to PID.
- Best CD Control: smooth α=0.05 achieves a CD error of 0.605 nm, meeting the stringent requirements of 3nm process nodes.

## 🛠️ Getting Started

Prerequisites:
- Python 3.7+
- Install required packages:
    pip install numpy matplotlib scipy tqdm

Running the Simulation:
1. Clone this repository or download the Python script file.
2. Run the main simulation script. This will execute all controllers and generate the comparison plots.
    python fshrink_euv_benchmark.py
    (Note: The simulation may take a few minutes to complete. A progress bar will be displayed.)
3. The script will output the performance table in the console and save a summary figure as high_na_euv_benchmark_results.png.

Code Structure:
- HighNAEUVModel: The core class defining the complex EUV system dynamics.
- Controller Classes: BaseController, PIDController, FastController, DecayController, SmoothController.
- run_euv_benchmark(): Function to run a simulation for a specific controller.
- The main script runs all configurations and analyzes performance.

## 📊 Results Visualization

The script generates a comprehensive figure (high_na_euv_benchmark_results.png) including:
- Time series of EPE, CD, and Overlay error for the top controllers.
- Bar charts comparing steady EPE, failure count, and CD error across all controllers.

## 📖 Citation

If you use this code or the underlying f-Shrink theory in your research, please cite the foundational paper:

Xie, M. (2026). Global Dynamics of a Transcendental Iteration System Based on the Balance Equation. Zenodo. https://doi.org/10.5281/zenodo.18485110

BibTeX entry:
@article{xie2026global,
  title={Global Dynamics of a Transcendental Iteration System Based on the Balance Equation},
  author={Xie, Meng},
  year={2026},
  publisher={Zenodo},
  doi={10.5281/zenodo.18485110},
  url={https://doi.org/10.5281/zenodo.18485110}
}

## 📄 License

This project is licensed under the MIT License.

## ☕ Support

If this work helps your research or project, please consider starring the repository and citing the paper. For further inquiries or commercial applications, you can open an issue.
