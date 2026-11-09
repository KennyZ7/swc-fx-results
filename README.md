# SWC-FX numerical results

CSV numerical records accompanying **SWC-FX: Conditioned Local–Memory Interaction for Real-Time Guitar Effect Modeling**, by Pengren Cheng, Communication University of China. Author ORCID: [0009-0007-2326-6273](https://orcid.org/0009-0007-2326-6273).

This is a data-only release of the existing, frozen numerical records. It contains **36 aggregate/evidence CSVs**, **51 formal model/seed per-example CSVs**, and **one model display-name mapping**. All 88 scientific CSVs are byte-identical to the corresponding entries in the existing 2026-11-08 submission-material archive. No model training, evaluation, bootstrap, checkpoint reselection or runtime measurement was performed for this release.

The companion manuscript is being prepared for submission; this release does not assign it a journal DOI or claim acceptance. **This GitHub release has no assigned data DOI.** Cite the versioned release or commit URL until a separate DOI-bearing archive exists.

## Files and starting points

| Location | Content |
|---|---|
| `tables/egfxset/main_results.csv` | Complete 12-model, three-seed EGFxSet summary |
| `tables/tonetwist/main_results.csv` | Complete five-model, three-seed ToneTwist summary |
| `tables/egfxset/holm_33_comparisons.csv` | All original 33 EGFxSet Holm comparisons |
| `tables/tonetwist/holm_12_comparisons.csv` | All original 12 ToneTwist Holm comparisons |
| `tables/egfxset/`, `tables/tonetwist/` | Seed, effect, family, rank, interval, configuration and training metadata tables |
| `tables/evidence/` | Nine supporting CSVs, including parameter comparisons, original effect differences, family summaries and Pi trial measurements |
| `reproducibility/formal_outputs/` | 51 formal model/seed per-example metric CSVs |
| `MODEL_DISPLAY_NAMES.csv` | Original experimental IDs and unique manuscript display names |
| `DATA_FILES.csv`, `SCHEMA.json` | Paths, roles, row counts, column names and hashes |
| `SHA256SUMS.txt` | File-integrity checksums for the release |

The 51 per-example files contain **32,976 model-example rows**: 36 EGFxSet model/seed runs with 901 test examples each, and 15 ToneTwist runs with 36 test examples each. These are repeated model measurements, not 32,976 independent performances. Original file layouts and column names are retained.

## Reading the records

The files are UTF-8 CSVs and can be read with a spreadsheet application or the Python standard-library `csv` module. Floating-point strings, confidence intervals, ranks, significance indicators, model IDs and checkpoint hashes are preserved without reformatting. There is no executable model or table-generation code in this data release.

`mrstft`, `mfcc_distance` and `rms_envelope_mae` are the three reported comparison metrics; lower is better. Overall results average clips equally within each seed and then average the three seed means. Other per-example diagnostics are inherited records and do not define additional headline rankings. See [DATA_DESCRIPTION.md](DATA_DESCRIPTION.md) for interpretation and evidence limits.

## Protocol and limitations

- EGFxSet uses 14 held-out string–fret groups; pickup/effect versions from a group remain together. ToneTwist has only two held-out performances, one bass and one guitar, with 30 distortion, two Clean and four modulation records.
- The two datasets were trained independently from initialization using seeds 41, 42 and 43. Historical seed41 W-only/I-only validation and the ToneTwist budget pilot remain explicitly separate from formal test results.
- Accuracy uses independent three-second clips, zero initial history/state and no warmup. This is not a new continuous paired-reference accuracy evaluation.
- Original 95% intervals and original Holm families (33 EGFxSet and 12 ToneTwist comparisons) are preserved. The intervals are not simultaneous Holm-adjusted intervals. No new statistical tests are introduced.
- SSM-27 is an approximate parameter match. GCN-TFiLM-R and LSTM64-R denote local adaptations under the recorded common protocol.
- Pi records include both the original configuration and the accepted configuration. Accepted trials are bound to EGFxSet SWC-FX seed41. Timing covers model callbacks and transition mixing, excluding device I/O, switch requests and reset; p99 is not round-trip audio latency or a universal hard-real-time guarantee.

## Source audio, rights and release boundaries

The original audio is obtained from the dataset providers, subject to their terms:

- EGFxSet: https://egfxset.github.io/
- ToneTwist AFx: https://github.com/mcomunita/tonetwist-afx-dataset

**No original audio, trained checkpoint tensors, model implementation source, manuscript PDFs, author submission records, credentials or workstation paths are distributed here.** Checkpoint hashes are identifiers, not checkpoint files. This dataset does not constitute a complete runnable training or evaluation distribution.

No additional reuse license is assigned by this release. Making these numerical records publicly inspectable does not relicense the original audio or other third-party material. Please cite the dataset release when referring to its results.

## Citation and provenance

Use [CITATION.cff](CITATION.cff) and the tagged release **v1.0.1**. The release date is **2026-11-09**. [PROVENANCE.json](PROVENANCE.json) identifies the source archive by its SHA256 without publishing local paths. The same CSV hashes appear in the frozen scientific bindings retained by the author. Public release is a packaging operation and does not change the scientific results.
