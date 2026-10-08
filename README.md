# VeMur Calcium Calculator

**VeMur Calcium Calculator** is a local, radiologist-supervised research workstation for coronary artery calcium (CAC) scoring on non-contrast CT.

It is designed for heterogeneous non-contrast CT data rather than only dedicated cardiac calcium-scoring acquisitions. VeMur evaluates acquisition and reconstruction parameters, prepares an appropriate measurement matrix when needed, detects calcium candidates, supports human review and vessel assignment, and exports the reviewed result together with protocol and methods information.

> **For Research Use Only — Not for Clinical Diagnosis**  
> VeMur Calcium Calculator is not intended to be used as a medical device or as the sole basis for diagnosis, patient management, or treatment decisions.

## Current public release

**VeMur Calcium Calculator v1.0.0 — Windows Standard / Light** is now available.

- [Download Windows x64 ZIP](https://github.com/memoend/VeMur-Calcium-Calculator/releases/download/v1.0.0/VeMur-Calcium-Calculator-1.0.0-windows-x64-standard-light.zip)
- [SHA-256 checksum file](https://github.com/memoend/VeMur-Calcium-Calculator/releases/download/v1.0.0/VeMur-Calcium-Calculator-1.0.0-windows-x64-standard-light.zip.sha256)
- [View release notes](https://github.com/memoend/VeMur-Calcium-Calculator/releases/tag/v1.0.0)

**SHA-256**

`7bfca9c261fd8a959eedd484d3115427419502be82217fce16853633e4b9c1bc`

Extract the entire ZIP before launching `VeMur-Calcium-Calculator.exe`. No separate Python installation is required.

## Highlights

- Local DICOM processing; no external image upload.
- Patient → Study → Series indexing with suggested-series prioritization.
- Quantitative HU conversion.
- Protocol-aware handling of kVp, reconstruction kernel, slice thickness, increment, and geometry.
- Native or research-standardized 3.0 mm measurement routing when appropriate.
- Controlled kernel normalization for predefined sharp-kernel conditions.
- Protocol-aware HU thresholds for supported tube-voltage profiles.
- Calcium-candidate detection with radiologist review and manual correction.
- STANDARD vessel estimation and optional DETAILED 3D localization.
- CSV, JSON, detailed report, annotated DICOM, MP4, and structured research exports.

## Why protocol-aware scoring?

Conventional Agatston scoring was developed for specific acquisition and reconstruction conditions. Routine non-contrast chest CT may differ in slice thickness, reconstruction increment, kernel, and tube voltage.

VeMur does **not** simply apply a fixed 130-HU / 3-mm assumption to every series. Instead, it records the acquisition, selects or prepares the measurement matrix, applies the active protocol profile, and exposes the resulting measurement identity in the report.

Examples:

- **Slice handling:** eligible thin-section data can be reconstructed into non-overlapping 3.0 mm scoring slabs.
- **Kernel handling:** predefined sharp-kernel conditions can be normalized for measurement using controlled Gaussian smoothing.
- **kVp handling:** supported non-120-kVp profiles use protocol-specific thresholds. The current ordinary 90-kVp research profile uses T1 = **162 HU** rather than 130 HU; this 90-kVp profile is an investigator-defined interpolation, not a universal clinical threshold.
- **Equivalent acquisitions:** recognized calcium-aware/equivalent conditions can be routed without unnecessary resampling.

The report records the measurement pathway. Depending on the active correction/routing path, VeMur may display an Agatston-equivalent identity such as **Agatston-KT**.

## Human-reviewed result

Automatic detections and vessel suggestions are assistance layers, not the final research endpoint.

Only lesions reviewed and assigned to LM, LAD, LCx, or RCA contribute to the reviewed coronary score.

| Key | Action |
| --- | --- |
| 1 | LM |
| 2 | LAD |
| 3 | LCx |
| 4 | RCA |
| 0 | Ignore |
| Enter | Accept selected suggestion |

## STANDARD and DETAILED

**STANDARD** is VeMur's lightweight built-in anatomy/geometric vessel-estimation workflow and is immediately available.

**DETAILED** uses the third-party SEGMENT-CACS 3D model for more detailed anatomic/vessel localization. It is optional, larger, and slower, and can be installed through **Setup / Repair**. Compatible GPU/CUDA hardware can substantially reduce runtime.

DETAILED does not replace the scoring mathematics or the radiologist review step.

## Quick start

- [Quick Start — English](docs/QUICK_START.md)
- [Hızlı Başlangıç — Türkçe](docs/QUICK_START_TR.md)

## Privacy

VeMur is designed as a local workstation. DICOM pixel data are processed locally and the application server binds to loopback for local use.

Researchers remain responsible for study-specific anonymization, ethics approval, data governance, and institutional requirements.

## License

Copyright © 2026 **Mehmet Erşen**. All Rights Reserved.

VeMur Calcium Calculator is distributed under the **VeMur Calcium Calculator Research Use License v1.0**.

- [LICENSE.txt](LICENSE.txt)
- [THIRD-PARTY-NOTICES.txt](THIRD-PARTY-NOTICES.txt)

## Citation

Citation metadata are available in [CITATION.cff](CITATION.cff).
