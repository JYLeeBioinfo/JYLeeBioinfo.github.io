---
title: "Using Rstudio with mamba-installed R"
date: 2023-10-02
categories: linux
---

## __1. Download and unzip Rstudio Tarball

 - Download tarball from : https://posit.co/download/rstudio-desktop/
   - I downloaded the following tarball for my CentOS 7 server
 ![image](https://github.com/hd00ljy/hd00ljy.github.io/assets/13775022/f1cb0ea9-7892-44f2-abcb-4eafd9a9d53f)

 - Unzip the tarball and change the owner and mode of chrome-sandbox
   - ```
     tar -zxf rstudio-2023.09.0-463-x86_64-fedora.tar.gz
     cd rstudio-2023.09.0+463
     # the following 2 commands are from the error message that shows up after executing rstudio right after the tarball unzipping.
     sudo chown root:root chrome-sandbox
     sudo chmod 4755 chrome-sandbox
     ls -l chrome-sandbox
     #-rwsr-xr-x. 1 root root 53840  Sep 26 09:16 chrome-sandbox
     ```
  
## __2. Download R using Conda or Mambaforge

 - I prefer to use conda/mamba to install R and R packages for easy installation and compatibility.
 - Mambaforge is better than plain conda nowadays because of the speed of package resolution and installation.
 - How to install and setup mambaforge : https://github.com/conda-forge/miniforge
 - create a conda environment and at the same time install R and R packages using mamba
   - ```
     mamba create -n cosmx -c conda-forge -c r -c bioconda r-base  r-seurat r-devtools r-terra r-magick
     ```


## __3. Environment Modules to easily set pathes
 - In order for Rstudio to recognize the R installed using conda/mamba, we need to set PATH,LD_LIBRARY_PATH, and CPATH (I haven't tested whether setting CPATH is essential or not)
 - The Enviroment Modules package makes it easy to dynamically load and unload those path settings.
 - Install Environment Modules : https://modules.readthedocs.io/en/stable/INSTALL.html
   - install tcl and tcl-devel if not already before installation.
     - ```
       yum install tcl tcl-devel
       ```
       
   - Download and install module files as described in the link : https://modules.readthedocs.io/en/stable/INSTALL.html
   - To use modulefile you need to source the profile. For me, I put it in the ~/.bashrc. I also set my custom MODULEPATH where modulefiles are stored.
     - ```
       #~/.bashrc
       source /usr/local/Modules/init/profile.sh
       export MODULEPATH=${MODULEPATH}:/home/hd00ljy/modulefiles/tools
       ```
       
   - make a modulefile
     - ```
       nano modulefiles/tools/cosmx/1
       ```
       
     - ```
       #%Module1.0

       proc ModulesHelp { } {
           puts stderr "              "
           puts stderr "\tThis module is for use of [module-info name]."
           puts stderr "              "
           puts stderr "\tYou need module(s): "
           puts stderr "\t              none "
           puts stderr "\tuse example: "
           puts stderr "\t    $ module load [module-info name]"
           puts stderr "              "
       }

       # install history
       #################################
       #mamba create -n cosmx -c conda-forge -c r -c bioconda r-base  r-seurat r-devtools r-terra r-magick
       #################################


       #if { [ module-info mode load ] } {
       #    module load gcc/7.4.0
       #}


       module-whatis   "loads the modules environment"

       # for Tcl script use only
       set      name            cosmx
       set      version         4.3.1
       set      envdir          /home/hd00ljy/mambaforge/envs
       set      prefix          $envdir/$name

       #if {![file exists $prefix]} {
       #    puts stderr "\t[module-info name] Load Error: $prefix does not exist"
       #    break
       #    exit 1
       #}

       prepend-path    PATH              $prefix/bin
       prepend-path    LD_LIBRARY_PATH   $prefix/lib/R/lib
       prepend-path    CPATH             $prefix/lib/R/include
       prepend-path    LD_LIBRARY_PATH   $prefix/lib
       prepend-path    CPATH             $prefix/include


       #if { [ module-info mode remove ] || [ module-info mode switch ]  } {
       #        module unload gcc/7.4.0
       #}
       
       ```
       
 - you can now load and unload conda-installed R(executables,libraries, and headers) using module command
   - ```
     module load cosmx/1 # load module
     module purge # unload all modules that have been loaded
     ```

## __4. Execute Rstudio
 - load module for conda/mamba-installed R
   - ```
     module load cosmx/1 # load module
     ```
     
 - Launch Rstudio
   - ```
     cd rstudio-2023.09.0+463
     ./rstudio
     ```

![image](https://github.com/hd00ljy/hd00ljy.github.io/assets/13775022/6c2ff68e-764b-491d-9a02-a3b23748fdb5)
