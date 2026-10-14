# Phase 1 Dataset Audit - GVLiD

Audit date: 2026-10-14
Dataset root: C:\MaxVoyage\Codes\GitHub\Major Project\DATASET

## Decision

Phase 1 is complete for dataset discovery and audit. The dataset is usable for Colab image-classification experiments, but it has important quality warnings that must be handled before training and before writing research claims.

## Basic Summary

- Total image files found: 3477
- Metadata records: 3477
- Metadata found for image files: 3477/3477
- Unique vineyards: 28
- Capture dates: {'2023-06-15': 3477}
- Latitude range: 18.731029 to 18.828946
- Longitude range: 73.971838 to 74.069959

## Folder-Label Class Counts

- Black Rot: 808
- Esca: 888
- Healthy: 1109
- Leaf Blight: 672

## Metadata Disease Counts

- Black Rot: 809
- Esca: 888
- Healthy: 1109
- Leaf Blight: 671

## Metadata Fields Available

- Filename
- Disease type / health status
- Capture datetime
- Vineyard ID
- GPS latitude and longitude
- Lighting category
- Categorical weather value: Clear, Humid, Windy
- Device name / sensor / OS

## Quality Warnings

- Folder labels and metadata.json disease labels disagree for 1344 images. For training, use label derived from the folder name and keep metadata_disease_type only for auditing unless manually corrected.
- Exact duplicate images are present: 446 duplicate hash groups, 1068 duplicate files beyond the first copy.
- Cross-class exact duplicates found in 2 duplicate groups. These must be removed or grouped before train/val/test splitting.
- All records have the same capture date: 2023-06-15. NASA POWER weather can still be queried by GPS/date, but temporal weather-window experiments will be weak because there is no date diversity.
- The dataset provides categorical weather labels, not numeric temperature/humidity/rainfall. Numeric weather must come from NASA POWER or another external weather source.

## Phase 2 Requirement

Before model training, build a leakage-safe split using duplicate groups and preferably vineyard groups. Do not randomly split individual images, because duplicate or near-duplicate images can leak across train/test.

Generated artifact: phase1_manifest.csv
