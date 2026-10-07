# VeMur Calcium Calculator — Quick Start

> **Research Use Only — Not for Clinical Diagnosis**

This guide describes the basic workflow of VeMur Calcium Calculator v1.0.

## 1. Open DICOM data

VeMur can open local DICOM data in three ways:

1. **Open DICOM Folder** — choose the study folder with the native Windows folder picker.
2. **Paste a local folder path** — paste the path and load it directly.
3. **Drag and drop** — drag a DICOM folder/files into the application when supported by the browser session.

VeMur first reads DICOM headers and builds a **Patient → Study → Series** list. Pixel data are decoded only after a series is selected.

![Open DICOM data](images/01-open-dicom.jpg)

## 2. Choose the most suitable series

If a study contains multiple CT series, VeMur evaluates the available metadata and can highlight a **Suggested** series for CAC measurement.

The suggestion helps with series selection; the user remains responsible for choosing the correct non-contrast CT series.

Factors considered include slice thickness, slice increment, reconstruction kernel, kVp, series description, and whether the series can be routed to an accepted measurement matrix.

## 3. Why the first series load may take longer

Opening the selected series starts the quantitative processing pipeline. VeMur may need to:

- decode DICOM pixel data,
- convert stored values to HU,
- evaluate slice geometry,
- select the active protocol profile,
- prepare a standardized 3.0 mm measurement matrix when required,
- apply predefined kernel normalization when required,
- detect calcium candidates,
- define the cardiac review region,
- and prepare vessel suggestions.

For this reason, a thin-section series with many images can take longer to open than ordinary image viewing.

## 4. Review calcium candidates

The **Calcium candidates** toolbar controls which overlays are displayed:

- **Cardiac** — candidates prioritized for cardiac/coronary review.
- **All** — all detector candidates.
- **Confirmed** — coronary calcium already confirmed by the reviewer.
- **None** — hides candidate overlays.

Automatic candidates are not the final score.

## 5. Assign coronary vessels

Select a candidate and assign it to the appropriate coronary vessel: **LM, LAD, LCx, or RCA**.

Keyboard shortcuts:

| Key | Vessel/action |
| --- | --- |
| 1 | LM |
| 2 | LAD |
| 3 | LCx |
| 4 | RCA |
| 0 | Ignore |
| Enter | Accept selected suggestion |

The vessel buttons and keyboard shortcuts operate on the selected candidate. Only reviewed lesions assigned to LM, LAD, LCx, or RCA contribute to the reviewed coronary score.

## 6. Manual ROI correction

If an automatic candidate is incomplete, incorrect, or absent, VeMur provides manual ROI tools including **Wand, Ellipse, and Curved ROI**.

A manually selected calcium region can be assigned to the required vessel. Manual measurements follow the active HU threshold profile used by the current scoring dataset.

## 7. STANDARD vs DETAILED vessel estimation

VeMur provides two vessel-estimation workflows.

### STANDARD

STANDARD is the built-in lightweight anatomy/geometric method.

- immediately available,
- fast,
- no additional model installation,
- intended to prioritize cardiac candidates and suggest likely vessel territories.

### DETAILED

DETAILED uses the third-party **SEGMENT-CACS** 3D model.

- optional,
- installed through **Setup / Repair**,
- larger and slower than STANDARD,
- designed for more detailed anatomic/vessel localization,
- benefits from compatible GPU/CUDA hardware when available.

DETAILED does **not** replace the calcium-scoring mathematics. It is an anatomic/vessel-localization aid, and the final result remains reviewer-controlled.

## 8. How VeMur adapts heterogeneous CT data

A major difference between VeMur and a conventional fixed-protocol calcium-scoring workflow is that VeMur evaluates the acquisition before measurement.

### Slice thickness and spacing

Eligible native acquisitions around accepted CAC geometry can be measured directly.

For eligible source data thinner than the target scoring geometry, VeMur can create a **research-standardized non-overlapping 3.0 mm measurement matrix** using physical z-axis integration.

Series thicker than the supported scoring geometry are not silently converted into a validated score; they are handled according to the application's scorability rules.

### Reconstruction kernel

A very sharp reconstruction can alter calcium appearance and HU behavior.

For predefined sharp-kernel conditions, VeMur can apply controlled **Gaussian normalization for measurement**. The source DICOM remains unchanged; the correction applies to the derived measurement pathway and is documented in the report.

### Tube voltage (kVp)

The conventional 120-kVp Agatston lower threshold is 130 HU.

For supported non-120-kVp research profiles, VeMur uses protocol-specific threshold boundaries. For example:

- **120 kVp:** T1 = 130 HU
- **ordinary 90-kVp research profile:** T1 = 162 HU

The current ordinary 90-kVp profile is an investigator-defined interpolation between selected 80- and 100-kVp profiles and should not be interpreted as a universal clinical standard.

### Equivalent/vendor-aware acquisition paths

Recognized calcium-aware/equivalent reconstruction conditions can be routed as an Agatston-equivalent measurement pathway without unnecessary 3-mm resampling.

## 9. Understand the score identity

VeMur reports not only the numeric score but also the measurement pathway used to produce it.

A conventional accepted native acquisition may be shown as **Agatston**.

When correction or equivalent-routing paths are active, the report can use an Agatston-equivalent identity. In the current interface, when both kernel and slice-thickness correction are active, the report may display:

**Agatston-KT — Kernel and Slice Thickness Corrected Agatston Equivalent**

## 10. Export results

Use the **Export** menu to create research outputs:

- CSV
- JSON
- detailed report
- annotated DICOM
- MP4 review material
- structured research data

![Export menu](images/06-export.jpg)

The detailed report documents the reviewed result together with the score identity, source slice thickness and increment, kVp, reconstruction kernel, active HU thresholds, standardization/normalization steps, and review status.

## Final principle

VeMur is intentionally **radiologist supervised**.

Automatic detection and vessel estimation are assistance layers. The final research result is the reviewed score after human confirmation and correction.
