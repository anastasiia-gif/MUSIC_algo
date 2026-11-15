# MUSIC Algorithm — Direction Finding & Distance Estimation with SDR

Implementation of the **MUSIC (MUltiple SIgnal Classification)** algorithm for radio direction-of-arrival estimation, together with distance estimation and the full signal-processing pipeline around it — from raw IQ samples to a clean MUSIC spectrum.

Everything lives in one documented Jupyter notebook: [`Music_distance_pre_post_processing.ipynb`](Music_distance_pre_post_processing.ipynb). Each stage is explained in markdown (what it is, why it's needed) and then implemented and visualized on test signals.

## Pipeline

**Pre-processing** of IQ data from the SDR:
- **DC offset removal** — real SDR hardware (KrakenSDR / RTL-SDR) leaves a non-zero mean on the I and Q components; this stage detects and removes it
- **Windowing** — reduces spectral leakage before frequency-domain processing
- **Band-pass filtering** — Butterworth filter isolating the signal band of interest

**Estimation:**
- **MUSIC** — direction-of-arrival estimation using the phase differences across a uniform linear antenna array (eigendecomposition of the covariance matrix, noise-subspace scan)
- **Distance estimation** with post-processing of the results

## Hardware

Tested with a KrakenSDR multi-channel receiver and an antenna array — see `Our_set_up.jpeg` for the physical setup and `Music_spectrum.JPG` for an example output spectrum.

## Running it

```bash
pip install numpy scipy matplotlib jupyter
jupyter notebook Music_distance_pre_post_processing.ipynb
```

The notebook generates synthetic test signals for every stage, so it runs end-to-end without any SDR hardware attached.
