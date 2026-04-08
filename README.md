# 🌲 Buçaco Canopy AI: 3D Forest Structural Analysis from 2D Satellite Imagery

<img width="934" height="381" alt="Captura de ecrã 2026-04-08 142145" src="https://github.com/user-attachments/assets/669f8007-d4ac-4290-8543-8739b3888580" />

### Project Overview
This repository contains a complete, end-to-end GeoAI pipeline for estimating tree canopy heights from standard 2D RGB imagery, bypassing the need for expensive LiDAR scans. By processing high-resolution satellite data through a self-supervised vision transformer, the script generates accurate 3D structural maps of forest environments. 

## Sourcing High-Resolution Custom Data
Instead of relying on pre-packaged sample datasets, I tested this model on a complex, real-world environment: the **Mata Nacional do Buçaco** in Portugal, known for its incredibly dense and ancient canopy. 

To achieve this without manual GIS downloads, the pipeline utilizes the `leafmap` library to programmatically connect to Google Satellite servers, extract high-resolution (zoom level 18) map tiles of the forest's bounding box, and stitch them together into a georeferenced TIFF file for analysis.

---

## Beyond the Baseline: Custom Analytics
While the core prediction engine relies on the established GeoAI pipeline, calculating a height map is only the first step. To make this data truly valuable for forestry management, I engineered three custom analytics modules:

### 1. Automated Giant Tree Detection
Calculating a continuous height map is only the baseline. To extract actionable insights, I engineered an automated spatial peak-detection algorithm. This module scans the generated topography of the canopy and mathematically isolates the coordinates of individual "giant" trees—specifically identifying structures towering over 30 meters—allowing forest managers to instantly map the oldest and largest specimens in the Buçaco forest.

<img width="820" height="799" alt="Captura de ecrã 2026-04-08 142202" src="https://github.com/user-attachments/assets/2490f6dc-cbe3-41e8-9c2b-ae7c1763d67c" />

### 2. Ecological Stratification Profiling
Forest ecology is defined by vertical layers, not just maximum height. To visualize the structural health of this ecosystem, I built a custom classification model that categorizes the AI-generated heights into distinct ecological zones: 
* **Understory:** 2 to 10 meters
* **Midstory:** 10 to 25 meters
* **Upper Canopy:** > 25 meters

This transforms a standard heatmap into a categorical map of forest architecture.

<img width="911" height="725" alt="Captura de ecrã 2026-04-08 151017" src="https://github.com/user-attachments/assets/a7e021b1-f9b4-4e29-abbe-c8049658bc54" />

### 3. Canopy Volume and Biomass Proxy
To translate raw pixel values into tangible physical metrics, I integrated a volumetric calculation module. By multiplying the physical area of each forested pixel by its predicted height, we can estimate the total cubic volume of the forest canopy across the analyzed region. This specific metric serves as a highly valuable proxy for estimating Above-Ground Biomass (AGB) and calculating the carbon storage potential of the forest.

---

## Installation & Setup

### Prerequisites
You will need Python installed along with the following geospatial and scientific libraries

## Usage
Simply open and run the Jupyter Notebook (`.ipynb`). The script handles data sourcing automatically; no raw satellite files need to be manually downloaded. The workflow is divided into logical steps:
1. Automated fetching of high-resolution satellite imagery via Bounding Box.
2. Initializing the compressed GeoAI Canopy model.
3. Generating and visualizing the 3D height map.
4. Running the custom peak-detection, stratification, and volumetric analytics.

---

## Acknowledgments & Credits

This project would not be possible without the incredible open-source tools and research provided by the geospatial community. 

* A special thank you to **Professor Qiusheng Wu** ([GitHub](https://github.com/giswqs)) for developing the `geoai` and `leafmap` Python libraries. His dedication to making complex Earth Observation tools accessible was the direct inspiration for this workflow.
* I also want to acknowledge **Tolan et al.** and the research team behind the original Meta *HighResCanopyHeight* model. Their groundbreaking work in utilizing self-supervised vision transformers to extract 3D canopy architecture from 2D RGB imagery provided the core machine learning engine for this analysis.
