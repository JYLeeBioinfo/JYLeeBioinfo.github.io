---
title: "using-mamba-to-install-R-and-Rstudio-desktop"
date: 2023-10-02
categories: linux
---

## 1. Download and install miniforge

 - Download miniforge : https://github.com/conda-forge/miniforge?tab=readme-ov-file#unix-like-platforms-mac-os--linux
   -  Run the following commmand tho install miniforge
     -  ```
        curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
        bash Miniforge3-$(uname)-$(uname -m).sh
        ```
  
## 2. Create environment with R and Rstudio Desktop using mamba

   - ```
     mamba create -n R -c conda-forge -c bioconda r-base r-devtools r-magick bioconductor-complexheatmap rstudio-desktop
     ```

## 3. Execute Rstudio
 - activate environment
   - ```
     mamba activate R
     ```
 - load module for conda/mamba-installed R
   - ```
     module load cosmx/1 # load module
     ```
     
 - Launch Rstudio
   - ```
     cd rstudio-2023.09.0+463
     ./rstudio
     ```
