# Non-Intrusive Load Monitoring on Indian Household Data (iAWE)

Energy disaggregation (Non-Intrusive Load Monitoring / NILM) on the iAWE Indian
household dataset — identifying individual appliance loads from an aggregate power
signal, with attention paid to India-specific grid behavior such as load-shedding and
simultaneous-restart events.

## Approach

- **Seq2Point CNN** vs. **1D Transformer**: two architectures compared for
  disaggregating aggregate power into per-appliance load estimates.
- **Vision Transformer on STFT spectrograms**: an additional variant that treats
  windows of the aggregate signal as time-frequency images.
- **End-to-end IoT pipeline**: an MQTT-based pipeline with live TFLite inference,
  demonstrating on-device deployment of the trained model.
- Handles three data-acquisition paths: a pre-existing `iawe.h5` file, raw CSVs
  converted via `nilmtk`, or synthetic iAWE-like data generated as a fallback when
  neither is available.

## Repo layout

- `nilm_iawe.ipynb` — the full pipeline: data loading, preprocessing, windowing, both
  model architectures, and the MQTT/TFLite deployment demo. This copy has been run
  end-to-end against the real iAWE data.
- `iawe.h5` — the real iAWE dataset, pre-converted from the official raw CSVs (tracked
  via Git LFS).
- `results/` — figures from a real run: the household's power-cut distribution and a
  week-long load trace.

## Setup

Designed to run on Google Colab, but `iawe.h5` is included directly in this repo so it
can also be run locally without a Drive mount. Install `nilmtk` if you'd rather convert
from raw CSVs yourself, or let the notebook fall back to synthetic data to explore the
pipeline without the real dataset.
