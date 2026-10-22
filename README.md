# Amazon River Outflow Along Coastal Brazil

This modeling project is an example to demonstrate the scope, files, and organization of a class project for CS 185C.

## Project Description

In this project, I investigate the impact of the Amazon River outflow on ocean conditions along the coast of Brazil. The central science question I aim to answer is:

**How does freshwater discharge from the Amazon River influence sea surface salinity and circulation along coastal Brazil?**

To explore this, I develop a high-resolution MITgcm ocean model centered on the northeastern coast of Brazil near the Amazon River mouth. The model is run for a representative period in 2008 using realistic bathymetry and forcing conditions. The experiment includes freshwater flux representing the Amazon discharge to examine its effects on salinity distribution and coastal dynamics.

Initial, boundary, and external forcing conditions are generated from ECCO Version 5 output for January 2008. River discharge is implemented as a surface freshwater flux. Results are analyzed through spatial and temporal plots of salinity, temperature, and current velocity fields.

## Reproducing Model Results

The following steps describe how to build the model files, set up and run the simulation on an HPC cluster, and analyze the output.

---

### Step 1: Create the Model Input Files

Generate the following input files using the listed Jupyter notebooks. These files should be saved to your `input/` directory:

- **Model Grid** – `Creating Model Grid.ipynb`  
- **Bathymetry** – `Bathymetry.ipynb`  
- **Initial Conditions** – `Creating Initial Conditions for Amazon Model.ipynb`  
- **External Forcing** – `Create External Forcing Conditions.ipynb`  
- **River Forcing** – `Amazon River Forcing.ipynb`  
- **Boundary Conditions** – `Boundary Conditions.ipynb`

These notebooks generate the binary `.bin` and metadata `.meta` files required by MITgcm.

---

### Step 2: Transfer Files to the HPC Cluster

1. Create a directory for your project:
   ```bash
   mkdir MITgcm/configurations/amazon_river
   ```

2. Use `scp` or another method to transfer the following directories to the cluster:
   - `input/`  
   - `code/`  
   - `namelist/`  

---

### Step 3: Compile the Model

On the HPC cluster, compile the model in a `build/` directory:

```bash
cd MITgcm/configurations/amazon_river
mkdir build
cd build
../../../tools/genmake2 -of ../../../tools/build_options/darwin_amd64_gfortran -mods ../code -mpi
make depend
make
```

---

### Step 4: Run the Model

1. Create a `run/` directory.
2. Link the input and executable files.
3. Submit the job script:
   ```bash
   sbatch cs185c13.slm
   ```

Ensure the `data.exf` file includes the river forcing and other surface forcing configurations as described in the external forcing and river forcing notebooks.

---

### Step 5: Analyze the Model Output

Use the following notebook to explore the model results:

- **Model Result.ipynb** – This notebook provides visualizations of surface salinity, temperature, and current patterns. It also includes time series plots and comparison of spatial anomalies to assess the impact of the Amazon River outflow on coastal oceanography.

---

This project helps illustrate how major freshwater sources like the Amazon River can influence coastal stratification, circulation, and salinity patterns in the western tropical Atlantic near Brazil.# darleneflower
