# Burnt area mapping using Sentinel-1 and Sentinel-2 Imagery

This project involves using Sentinel-1 and Sentinel-2 imagery to accurately measure and analyze fire events happened in Quebec province, Canada in 2023. The process includes pre-processing steps like terrain correction and speckle filtering for Sentinel-1 SAR data and cloud masking and atmospheric correction for Sentinel-2 optical data. 

## Ground Truth Data

- **Loading Ground Truth Data**: Importing ground truth data indicating fire presence.
- **Creating Ground Truth Raster**: Creating a binary raster of fire presence.
- **Visualizing Ground Truth**: Displaying the ground truth fire map on the map.

  
## Sentinel-1 Image Processing

### Terrain Correction

The `terrainCorrection` function applies radiometric terrain correction to Sentinel-1 images to correct distortions caused by terrain variations. This involves:
1. **Loading SRTM DEM Data**: Using the SRTM DEM to understand terrain variations.
2. **Radar and Terrain Geometry Calculations**: Calculating radar and terrain geometry such as slope and aspect.
3. **Local Incidence Angle Calculation**: Computing the local incidence angle.
4. **Gamma0 Calculation**: Correcting the backscatter coefficient (Gamma0).
5. **Volumetric Model Application**: Applying a volumetric model to account for volume scattering effects.
6. **Layover and Shadow Masking**: Masking areas affected by layover and shadow.

### Speckle Filtering

The `refinedLee` function applies the Refined Lee Speckle Filter to Sentinel-1 images to reduce speckle noise while preserving edges and features. This process involves:
1. **Kernel Creation**: Setting up 3x3 and 7x7 kernels for local statistics.
2. **Mean and Variance Calculation**: Calculating mean and variance for the image.
3. **Gradient and Direction Determination**: Finding gradients and directions to identify maximum gradients.
4. **Directional Statistics Calculation**: Using directional kernels to compute local statistics.
5. **Filtered Value Calculation**: Generating the filtered value based on local statistics.

### Sentinel-1 Image Collection

- **Pre-Fire and Post-Fire Image Collection**: Filtering Sentinel-1 images for pre-fire (2023-05-07 to 2023-05-08) and post-fire (2023-11-03 to 2023-11-04) periods.
- **Terrain Correction and Speckle Filtering**: Applying terrain correction and refined Lee filter to pre-fire and post-fire images.
- **Log-Ratio Calculation**: Computing the log-ratio for VV and VH polarizations to identify changes.

## Sentinel-2 Image Processing

### Cloud Masking

The `maskClouds` function masks clouds using the QA60 band of Sentinel-2 images. This involves:
1. **Cloud Bit Masking**: Masking cloud and cirrus pixels.

### Atmospheric Correction

The `dos` function applies Dark Object Subtraction (DOS) for atmospheric correction. This involves:
1. **Dark Object Calculation**: Computing dark object values for each band.
2. **Subtracting Dark Objects**: Correcting the image by subtracting dark object values.

### Sentinel-2 Image Collection

- **Pre-Fire and Post-Fire Image Collection**: Filtering Sentinel-2 images for pre-fire (2023-04-08 to 2023-04-09) and post-fire (2023-12-04 to 2023-12-05) periods.
- **Creating Composites**: Creating median composites for pre-fire and post-fire images.
- **Atmospheric Correction**: Applying DOS atmospheric correction to pre-fire and post-fire images.

### NBR and dNBR Calculation

- **NBR Calculation**: Calculating the Normalized Burn Ratio (NBR) for pre-fire and post-fire images.
- **dNBR Calculation**: Computing the differenced NBR (dNBR) to identify burn severity.

## Visualization

- **Map Layers**: Adding various layers to the map including raw images, terrain corrected images, speckle filtered images, log-ratio images, ground truth fire map, NBR, and dNBR.

## Results

- **Pre-Fire and Post-Fire Analysis**: Visualizing and comparing pre-fire and post-fire conditions using Sentinel-1 and Sentinel-2 imagery.
- **Fire Detection**: Identifying areas affected by fire using log-ratio and dNBR analysis.

## Instructions

1. **Run the Script**: Execute the provided script in Google Earth Engine to perform the described processing steps.
2. **Explore Results**: Examine the resulting layers on the map to analyze the impact of fire events.

## Dependencies

- **Google Earth Engine**: The script is designed to run on the Google Earth Engine platform.

## Credits

- **Terrain Correction**: Implementation by Andreas Vollrath (ESA), inspired by Johannes Reiche (Wageningen).
- **Refined Lee Filter**: Implementation based on standard Refined Lee filtering techniques.

---

This README provides an overview of the processing steps and methods used in this project for fire detection and analysis using Sentinel-1 and Sentinel-2 imagery on the Google Earth Engine platform.

