# RIBOmap_pipe
**RIBOmap** is a protocol for spatial translatome mapping. This pipeline is implemented in **Jupyter Notebooks**, providing an interactive environment for reproducible analyses including such steps as image registration, stitching, cell segmentation and read assignment according to [].


**Steps**
1. **Deconvolution**  - is used to minimize out-of-focus background . In this repo [sparse-deconv-py](https://github.com/WeisongZhao/sparse-deconv-py) is used , see notobook [link]
   <img width="1230" height="730" alt="image" src="https://github.com/user-attachments/assets/485f1740-da33-43e8-97e0-fc40922a97e3" />

3. **Image Registration and Reads extraction** Use [starfinder](https://github.com/wanglab-broad/starfinder) as in []. You need previously install

Create starfinder enviroment:
  ```
  conda env create --file config/environment.yaml
  
  ```
  Run using starfinder & MATLAB:
  
  ```
  addpath('./code-base/src', './example/sequential_workflow')
  rsf_workflow_example('~/sample-dataset/tissue-2D/dataset-info.
  json')
  ```
3. **Stitching** is the process of combining multiple images or image fragments into a single large, seamless image. This repo contains jupyter notebook[] with ability to run pyimagej as script without GUI.

4. **Merging detected amplicon signals of each FOV**
   Run using starfinder & MATLAB:
  ```
  reads_stitching('~/sample-dataset/tissue-2D/dataset-info.json')
  quit()
  ```
Next, you can choose which segmentation method you want to use, or try both and select the best one (recommended):

1. **StarDist [link]**
2.  **ClusterMap [link]**
