---
title: "How to connect multiple versions of R to jupyterlab"
output:
  html_document: default
date: "2024-12-16"
---

Note : The page is based on ChatGPT response but edited and tested by me.

To add **additional versions of R** to JupyterLab, you need to install and register each R version as a separate Jupyter kernel using `IRkernel`. This allows you to switch between different R versions within JupyterLab.

---

## Steps to Add Multiple R Versions

### 0. **Set Up JupyterLab Environment**
Make sure you install JupyterLab in advance and set or activate the environment where you can launch JupyterLab.

```bash
# UTK ISAAG-NG
module load anaconda3/2023.09
# or other environment settings for your jupyter installation
```

### 1. **Install Mutiple R Versions**
Make sure you have all the R versions you need installed on your system. You can install them side-by-side and access them via their respective paths.

For example:
- `R-3.6.3` might be installed as `/usr/local/bin/R-3.6.3`
- `R-4.2.0` might be installed as `/usr/local/bin/R-4.2.0`

---

### 2. **Install IRkernel for Each R Version**
Launch each R version **individually** and install the `IRkernel` package.

#### For R Version 3.6.3
Run the following in the R console:
```r
install.packages("IRkernel")
IRkernel::installspec(name = 'ir363', displayname = 'R 3.6.3', user = FALSE)
```
- installspec function of IRkernel creates configuration files which jupyter reads to set up kernels.
- `name`: Unique kernel name for Jupyter.
- `displayname`: The name that will appear in JupyterLab.
- user = TRUE if you do not have root privilege, which will be the most common case.

#### For R Version 4.2.0
Launch R 4.2.0 and run:
```r
install.packages("IRkernel")
IRkernel::installspec(name = 'ir420', displayname = 'R 4.2.0', user = FALSE)
```

---

### 3. **Verify Kernel Installation**
After installing the kernels for each R version, list the available kernels to verify:

```bash
jupyter kernelspec list
```

The output should look like this:

```
Available kernels:
  python3      /usr/local/share/jupyter/kernels/python3
  ir363        /usr/local/share/jupyter/kernels/ir363
  ir420        /usr/local/share/jupyter/kernels/ir420
```

---

### 4. **Launch JupyterLab**
Start JupyterLab:

```bash
jupyter lab
```

When creating a new notebook, you will see multiple R options in the "New" dropdown or under "Kernel" > "Change Kernel":

- **R 3.6.3**
- **R 4.2.0**

You can now select the version of R you want to use.


FYI, this is how it looks like in the JupyterLab

![image](https://github.com/user-attachments/assets/d0bbce40-a35f-4b18-b8ac-c11ac15beea5)


---

### Notes:
- Each version of R must have `IRkernel` installed separately.
- Use unique names (`name` parameter) for each R kernel to distinguish them in Jupyter.
- If you install a new R version later, simply repeat the above steps for that version.
