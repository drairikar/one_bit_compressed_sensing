# One-Bit Compressed Sensing on MNIST

Recovering sparse signals and MNIST digit images from **1-bit measurements** y = sign(Φx). Each
measurement keeps only its sign, so all amplitude information is lost. Four reconstruction algorithms are
compared as the measurement ratio M/N goes from 0 to 2.

Group project, MSc Electrical Engineering, TU Delft
(original repository: [iandlg/one_bit_compressed_sensing](https://github.com/iandlg/one_bit_compressed_sensing)).

## Algorithms (`src/`)

| File | Method |
| --- | --- |
| `biht_l1.m` | **BIHT**: binary iterative hard thresholding (Jacques, Laska, Boufounos & Baraniuk) |
| `obbcs.m` | **One-bit Bayesian CS** with sign-flip robustness (Li, Fang, Li et al., IEEE SPL 2015) |
| `one_bit_lp.m` | Convex LP relaxation with a total-variation term (CVX) |
| `one_bit_bp.m` | One-bit basis pursuit with a total-variation term (CVX) |

Helpers: `gen_data.m` (synthetic K-sparse signals with optional sign flips), `get_stats.m` (NMSE, computed on
unit-normalised vectors because 1-bit CS only recovers the direction of x, and output SNR, which is not
normalised and therefore depends on the reconstructed amplitude), `sgn.m`,
`f_lambda.m`.

## Experiments (`src/main.m`)

1. **Synthetic**: N = 51, K = 5, M = 100. All four algorithms on the same draw.
2. **MNIST**: 28 × 28 digits, Gaussian sensing matrices with unit-norm columns, M/N ∈ [0, 2].
   Reconstruction quality (SNR, NMSE) is plotted against M/N for each method.

## Running

Requires MATLAB with [CVX](https://cvxr.com/cvx/) and the Statistics and Signal Processing toolboxes
(`random`, `snr`). Put `mnist.mat` in `src/` (it is not committed), then run the script below; figures are
written to `output/`.

```matlab
cd src
main
```
