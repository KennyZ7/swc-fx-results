# Data description

## Scope of a record

The aggregate/evidence tables contain 36 CSV files (27 dataset tables plus nine cross-dataset/deployment evidence tables). The per-example directory contains 51 CSV files, one per formal model/seed run. `MODEL_DISPLAY_NAMES.csv` is a separate mapping file. `DATA_FILES.csv` lists the number of rows and SHA256 of every scientific CSV; `SCHEMA.json` lists its original column names.

## Common fields

| Field or suffix | Meaning |
|---|---|
| `model`, `model_id`, `candidate`, `baseline` | Original experimental IDs; use the display-name map for manuscript labels |
| `display_name`, `*_display_name` | Descriptive manuscript names; not new experimental variants |
| `seed` | Training seed; formal runs use 41, 42 and 43 |
| `id` | Existing evaluation-pair identifier, not a raw audio waveform or person identifier |
| `effect_id`, `effect_family` | Existing target-effect and family identifiers |
| `performance_group` | Paired resampling/grouping key; versions within one group are correlated |
| `parameter_count`, `*_parameters` | Trainable parameter count under the corresponding dataset vocabulary |
| `mrstft`, `mrstft_mean` | Mean multi-resolution log-magnitude spectral error; Hann windows 512/1024/2048 with quarter-window hops |
| `mfcc_distance`, `mfcc_distance_mean` | Mean absolute difference of 20 MFCC coefficients including c0; recorded analysis is 2048/512 with 80 Slaney bands |
| `rms_envelope_mae`, `rms_envelope_mae_mean` | RMS envelope mean absolute error; recorded analysis is 4096/1024 |
| `std`, `sample_sd`, `*_std` | Recorded sample SD across the three seed-level clip means, where applicable |
| `*_variance` | Recorded seed-level variance; not recomputed for this release |
| `ci95_low`, `ci95_high`, `*_ci95_*` | Original 95% bootstrap endpoints for the quantity named in that table |
| `mean_difference`, `original_mean_difference` | Paired baseline-minus-SWC-FX error; positive favors SWC-FX where specified by `direction` |
| `raw_p`, `holm_p`, `original_*p` | Original raw/adjusted p values; the recorded family size and significance flags are retained |
| `favorable_and_significant`, `original_favorable_and_significant` | Original favorable-direction and Holm p<0.05 flag |
| `rank`, `descriptive_rank` | Recorded per-metric rank; there is no composite ranking; family ranks are descriptive |
| `checkpoint_sha256`, `teacher_sha256`, `initialization_sha256` | Hash identities, not redistributed model tensors |
| `selected_epoch`, `completed_epochs`, `termination`, `stop_reason` | Original training/selection metadata; actual stopping epochs may differ by model |
| `architecture`, `architecture_display`, `model_config_json` | Original configuration and separate display wording; older raw field terminology is retained |
| `profile`, `trial` | Recorded deployment configuration and trial identity |
| `steady_*`, `switch_*` | Steady-state and transition callback timing/counters under the stated configuration |
| `xrun_*`, `io_*`, `short_io_*`, `recovery_*` | Recorded audio-I/O and recovery counters |

For all columns and row counts, consult `SCHEMA.json`; the files deliberately keep their original, dataset-specific schema. Blank fields remain blank. Additional inherited per-example fields (`esr`, `spectral_convergence`, `lsd_db`, `l1`, `preemphasis_l1`, `highfreq_lsd_db`, `long_envelope_l1`, `late_tail_esr`, `spectral_flux_l1`, `mae`) are retained as diagnostic records. They are not newly validated outcomes or replacements for the three manuscript metrics. In particular, a late-segment metric is not evidence of a detected natural stop-playing tail.

## Comparison units

EGFxSet: 12 models × 3 seeds × 901 held-out examples, grouped into 14 string–fret groups. ToneTwist: 5 models × 3 seeds × 36 held-out examples from two performances. Bootstrap repetitions, effect versions and repeated model outputs do not create new independent performances or training seeds.

Results concern fixed recorded target settings and known conditions. Independent three-second tests start from zero history/state. Existing prehistory omitted by this protocol is not restored by C++ parity or the Pi runtime trials. Parameter counts do not measure comparative runtime, peak memory or training compute.

The historical validation ablation and development pilot are released for context, not silently added to the formal test matrix. Original numeric strings, ranks, intervals and Holm decisions are untouched.
