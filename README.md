# SpatialOmics-RNA-Pipe
**Status:** To be updated ⚠️

This repository provides a fully integrated, reproducible, and interactive Jupyter Notebook-based pipeline for spatial omics data analysis. It supports major steps including deconvolution, image registration, stitching, cell segmentation, and read assignment, enabling users to generate spatially resolved single-cell RNA and protein profiles.

The pipeline is compatible with methods such as STARmap PLUS, RIBOmap, and TEMPOmap, allowing researchers to explore spatial and temporal RNA dynamics in heterogeneous cells and tissues. Designed for ease of use, it leverages sparse-deconv-py, starfinder, and StarDist for high-quality, reproducible results.

Users can follow guided notebooks to process raw microscopy images into single-cell spatial transcriptome and translatome maps, making this toolkit ideal for both novice and experienced spatial omics researchers.

**SpatialOmics-RNA-Toolkit** is a protocol for spatial translatome mapping. This pipeline is implemented in **Jupyter Notebooks**,  according to [https://www.nature.com/articles/s41596-025-01248-3](https://www.nature.com/articles/s41596-025-01248-3).


**Steps**
1. **Deconvolution**  - is used to minimize out-of-focus background . In this repo [sparse-deconv-py](https://github.com/WeisongZhao/sparse-deconv-py) is used , see notobook [1.deconvolution.ipynb](1.deconvolution.ipynb)
   <img width="1230" height="730" alt="image" src="https://github.com/user-attachments/assets/485f1740-da33-43e8-97e0-fc40922a97e3" />

3. **Image Registration and Reads extraction** Use [starfinder](https://github.com/wanglab-broad/starfinder) as in []. You need previously install ***MATLAB 2023b or newer*** and create starfinder enviroment:
  ```
  conda env create --file config/environment.yaml
  
  ```
  Run using starfinder & MATLAB:
  
  ```
  addpath('./code-base/src', './example/sequential_workflow')
  rsf_workflow_example('~/sample-dataset/tissue-2D/dataset-info.
  json')
  ```
3. **Stitching** is the process of combining multiple images or image fragments into a single large, seamless image. This repo contains jupyter notebook [2.stitching_and_pyimage_steps.ipynb](2.stitching_and_pyimage_steps.ipynb) with ability to run pyimagej as script without GUI.

4. **Merging detected amplicon signals of each FOV**
   Run using starfinder & MATLAB:
  ```
  reads_stitching('~/sample-dataset/tissue-2D/dataset-info.json')
  quit()
  ```
5. **Cell segmentation and read assignmnets**
   <p float="left">
  <img src="https://github.com/user-attachments/assets/aae9c8b1-cdd1-4955-b40e-0dcf27ae76ab" width="500px"/>
  <img src="https://github.com/user-attachments/assets/b96c5afd-f372-4215-8327-a8057f1c9cf2" width="750px"/>
</p>
<!-- ![telegram-cloud-photo-size-2-5246939676562624440-y](https://github.com/user-attachments/assets/aae9c8b1-cdd1-4955-b40e-0dcf27ae76ab)
<img width="1000" height="1000" alt="eacb9fad1ecd7a6650e9d12f8a9de50f" src="https://github.com/user-attachments/assets/b96c5afd-f372-4215-8327-a8057f1c9cf2" /> -->


   Next, you can choose which cell segmentation method you want to use, or try both and select the best one (recommended):

   - **[StarDist](https://github.com/stardist/stardist)**
     1) For StarDist segmentation firstly run step 2. Fused DAPI staining and sequencing image in   [2.stitching_and_pyimage_steps.ipynb](2.stitching_and_pyimage_steps.ipynb) for receiving overlay.tif image
     2) Next use [3.stardist_segmentation.ipynb](stardist_segmentation.ipynb) for cell segmentation
     3) For read assigment move on to starfinder enviroment and run following script. Before running script move on your genes.csv and grid.csv to documents subdirectory:
        ```conda activate starfinder
            python example/sequential_workflow/reads_assignment.py ~/sample-dataset/tissue-2D/datasetinfo.json
        ```
   - **[ClusterMap](https://github.com/wanglab-broad/ClusterMap)**
  
     Before running ClusterMap copy your genes.csv and grid.csv to documents subdirectory. The run following commands:
     First for cell segmentation of each tile:
      ``` conda activate starfinder
         python example/sequential_workflow/run_clustermap.py ~/sample-dataset/tissue-2D/datasetinfo.json
      ```
      Then stitch them and read assignments:
     
      ```
         python example/sequential_workflow/stitch_clustermap.py ~/sample-dataset/tissue-2D/dataset-info.json
      ```
