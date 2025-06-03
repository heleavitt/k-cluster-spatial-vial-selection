CAREER Isotope Wrapping Selector
Author: Herbert Leavitt
Last Updated: November 15, 2024

Purpose:
This R Markdown workflow selects unwrapped isotope samples across habitat gradients for targeted processing. It ensures balanced sampling by species and habitat (mangrove edge quartiles), excludes duplicates, and prioritizes underrepresented clusters based on spatial k-means.

Requirements:
R Packages:
- tidyverse
- sf
- readxl
- gsheet
- raster
- janitor
- knitr (for rendering)

File Structure & Inputs:
The script relies on files from three main directories:

1. sharepoint_landing/ (raw inputs)
- wrapping_inventory.csv
- drop_sample_tracking.xlsx

2. landscape_species_scale/SP23/landscape_analysis/output/
Species-specific habitat CSVs:
- satscale/google2022_edge1_buf300.csv
- smallscale/combined_2022_edge1_buf50.csv
- ... (one per species/buffer/edge combo in species_params)

3. raw_input/shapefiles/
- PtFou2020crop.tif

4. isotope_workflow/sample_selection/selected samples/SP23/
- wrapping_table_250515.csv  (Required if rerunning after selection)

Workflow Summary:
1. Data Import
2. Filtering
3. Habitat Join
4. Quartile Assignment
5. Deficit Calculation
6. Spatial Clustering (k-means)
7. Selection & Export

Notes & Assumptions:
- All habitat CSVs must exactly match the naming pattern expected.
- Raster file PtFou2020crop.tif must exist and be in EPSG:4326.
- Variables like old_table, slim_old must be loaded if used.
- Biomass threshold > 0.02 g.
- K-means uses 5 clusters.

Outputs:
- wrapping_table_250515.csv: List of vials to wrap.
- composite_prep_250515.csv: Mass contribution breakdown per site/species.

Suggested Improvements:
- Add file checks using file.exists().
- Modularize chunks into functions.
- Move hard-coded paths to a config section.
- Cache habitat files to reduce redundant reads.
