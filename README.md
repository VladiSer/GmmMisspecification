# The Interplay of Signal-to-Noise Ratio and Variance Misspecification in Gaussian Mixtures

MATLAB code accompanying the paper:

> **The Interplay of Signal-to-Noise Ratio and Variance Misspecification in Gaussian Mixtures**

---

## Repository layout

```
GMM-Variance-Misspecification/
├── Shared/                       shared utilities (GetScientistImageData, Scientists/)
├── FiniteSampleExperiment/       empirical K-means & EM finite-sample simulation
├── PopulationEM_GHQuadrature/    population-level EM via GH quadrature
└── TheoreticalAndEmpiricalK2Gmm/ analytical & Monte Carlo centroid MSE demos
```

Each module is self-contained with its own `ExampleRun.m` and `README.md`.

---

## Modules

### FiniteSampleExperiment
Runs K-means and EM on a synthetic GMM whose centroids are scientist portrait
images, sweeping SNR from −25 dB to +25 dB.  Records classification accuracy
and normalised centroid MSE over many Monte Carlo averages.

→ See [`FiniteSampleExperiment/README.md`](FiniteSampleExperiment/README.md)

### PopulationEM_GHQuadrature
Computes the one-step population EM update from ground truth by integrating
over the true data distribution using Gauss-Hermite quadrature.  Sweeps over
a 2-D grid of SNR × misspecification ratio τ/σ to produce the paper's MSE
heat-maps.

→ See [`PopulationEM_GHQuadrature/README.md`](PopulationEM_GHQuadrature/README.md)

### TheoreticalAndEmpiricalK2Gmm
Closed-form and Monte Carlo scripts that build intuition: shows how the
hard-assignment centroid estimator under a symmetric 2-component GMM
transitions from unbiased (MSE ∝ σ²) to saturated as σ grows, and
visualises the centroid trajectory projected onto the separation axis.

→ See [`TheoreticalAndEmpiricalK2Gmm/README.md`](TheoreticalAndEmpiricalK2Gmm/README.md)

---

## Quick start

Each module is independent.  Pick the one relevant to you, `cd` into it, and
run its `ExampleRun.m`:

```matlab
% --- empirical simulation ---
cd FiniteSampleExperiment
SetPaths
run ExampleRun

% --- population-level analysis ---
cd PopulationEM_GHQuadrature
run ExampleRun

% --- analytical & Monte Carlo ---
cd TheoreticalAndEmpiricalK2Gmm
run ExampleRun
```

---

## Dependencies

| Toolbox | Required by |
|---|---|
| Statistics and Machine Learning Toolbox | FiniteSampleExperiment (`fitgmdist`), PopulationEM (`sobolset`, `norminv`) |
| Parallel Computing Toolbox | FiniteSampleExperiment (`parfor`), PopulationEM (`parfor`) — optional |
| MATLAB R2021b or later | `matchpairs` used in FiniteSampleExperiment and PopulationEM |

The Crameri scientific colourmap (`crameri.m`, `CrameriColourMaps7.0.mat`)
is included inside `PopulationEM_GHQuadrature/` and requires no separate
installation.

---

## Notation used throughout the code

| Symbol | Meaning |
|---|---|
| K | number of mixture components |
| D | data dimension (= `imageSize²` for image experiments) |
| N | number of observations |
| σ | true noise standard deviation |
| τ | fitted (misspecified) noise standard deviation |
| τ/σ | misspecification ratio (= 1 means correctly specified) |
| SNR | signal-to-noise ratio in dB: 20 log₁₀(‖μ‖/σ) |

Variable naming conventions in the code:  
`v` — vector · `m` — matrix · `s` — struct · `vs` — vector of structs ·  
`ca` — cell array · `b_` — boolean · `n` — scalar count · `i` — loop index
