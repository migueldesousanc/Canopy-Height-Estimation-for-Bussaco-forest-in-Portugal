# 🌲 Buçaco Canopy AI: 3D Forest Structural Analysis from 2D Satellite Imagery

![Header Dashboard](images/header_dashboard.png)
*(Drop a screenshot of your side-by-side satellite and predicted canopy height maps here, and name it `header_dashboard.png`)*

### Project Overview
This repository contains a complete, end-to-end GeoAI pipeline for estimating tree canopy heights from standard 2D RGB imagery, bypassing the need for expensive LiDAR scans. By processing high-resolution satellite data through a self-supervised vision transformer, the script generates accurate 3D structural maps of forest environments. 

## 🛰️ Sourcing High-Resolution Custom Data
Instead of relying on pre-packaged sample datasets, I tested this model on a complex, real-world environment: the **Mata Nacional do Buçaco** in Portugal, known for its incredibly dense and ancient canopy. 

To achieve this without manual GIS downloads, the pipeline utilizes the `leafmap` library to programmatically connect to Google Satellite servers, extract high-resolution (zoom level 18) map tiles of the forest's bounding box, and stitch them together into a georeferenced TIFF file for analysis.

---

## 🚀 Beyond the Baseline: Custom Analytics
While the core prediction engine relies on the established GeoAI pipeline, calculating a height map is only the first step. To make this data truly valuable for forestry management, I engineered three custom analytics modules:

### 1. Automated Giant Tree Detection
Calculating a continuous height map is only the baseline. To extract actionable insights, I engineered an automated spatial peak-detection algorithm. This module scans the generated topography of the canopy and mathematically isolates the coordinates of individual "giant" trees—specifically identifying structures towering over 30 meters—allowing forest managers to instantly map the oldest and largest specimens in the Buçaco forest.

![Giant Tree Detection](images/giant_trees.png)
*(Drop a screenshot of the satellite map with the red circles around the giant trees here, and name it `giant_trees.png`)*

### 2. Ecological Stratification Profiling
Forest ecology is defined by vertical layers, not just maximum height. To visualize the structural health of this ecosystem, I built a custom classification model that categorizes the AI-generated heights into distinct ecological zones: 
* **Understory:** 2 to 10 meters
* **Midstory:** 10 to 25 meters
* **Upper Canopy:** > 25 meters

This transforms a standard heatmap into a categorical map of forest architecture.

![Forest Stratification](images/stratification_profile.png)
*(Drop a screenshot of the 3-color stratification map here, and name it `stratification_profile.png`)*

### 3. Canopy Volume and Biomass Proxy
To translate raw pixel values into tangible physical metrics, I integrated a volumetric calculation module. By multiplying the physical area of each forested pixel by its predicted height, we can estimate the total cubic volume of the forest canopy across the analyzed region. This specific metric serves as a highly valuable proxy for estimating Above-Ground Biomass (AGB) and calculating the carbon storage potential of the forest.

---

## 🛠️ Installation & Setup

### Prerequisites
You will need Python installed along with the following geospatial and scientific libraries:

```bash
pip install geoai-py leafmap rasterio scikit-image matplotlib numpy

