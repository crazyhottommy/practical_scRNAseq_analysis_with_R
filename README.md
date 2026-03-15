# Practical scRNAseq Analysis with R

A hands-on course for single-cell RNA-seq analysis using R. We work through a real PBMC dataset (GSE126030) from raw sequencing data to biological interpretation.

**Book**: https://crazyhottommy.github.io/practical_scRNAseq_analysis_with_R/

## What's covered

1. **Data download and quantification** - simpleaf/alevin-fry (Chapter 1)
2. **Quality control** - empty droplet removal with DropletUtils (Chapter 2)
3. **Seurat workflow** - normalization, integration, clustering, UMAP (Chapter 3)
4. **Cell annotation** - SingleR, clustifyr, label transfer (Chapter 4)
5. **Gene set analysis** - GSEA with clusterProfiler (Chapter 5)

## Setup instructions

### Prerequisites

- **R >= 4.3.0** (for Bioconductor 3.18+)
- **RStudio** (latest version)
- **Git**

**Windows users**: Install [Rtools](https://cran.r-project.org/bin/windows/Rtools/) before step 3 below. Chapter 1 (quantification with simpleaf) requires a Unix environment, so you can skip it and start at Chapter 2 using the pre-processed data.

**macOS users** (if you hit compilation errors):

```bash
brew install libxml2 openssl curl libgit2
```

**Ubuntu/Debian**:

```bash
sudo apt-get install -y \
  libxml2-dev libssl-dev libcurl4-openssl-dev \
  libfontconfig1-dev libfreetype6-dev libpng-dev \
  libtiff5-dev libjpeg-dev libharfbuzz-dev \
  libfribidi-dev libgit2-dev
```

### Step 1: Clone the repo

```bash
git clone https://github.com/crazyhottommy/practical_scRNAseq_analysis_with_R.git
```

### Step 2: Open the project

Open `bookdown-demo.Rproj` in RStudio. You should see a message about renv being activated.

### Step 3: Install packages

```r
# If you don't have renv yet:
install.packages("renv")

# Install all packages at the exact versions used in the course:
renv::restore()
```

This takes 30-60 minutes. Bioconductor packages are slow to compile. Go get lunch.

### Step 4: Download the data

Download the data zip file (~540MB) from Google Drive:

https://drive.google.com/file/d/1944UsXcu-vZqm39wk76xtUlBRRacX0o-/view?usp=sharing

Unzip it and place the contents into the `data/` folder in the project directory. You should end up with:

```
data/
  SRX5329394_quant/
  SRX5329395_quant/
  SRX5329396_quant/
  SRX5329397_quant/
  pbmc_seurat_obj.rds
  ref.Rds
```

### Step 5: Work through the chapters

Open the Rmd files in order and run the code chunks interactively. Each chapter saves intermediate objects, so you can start at any chapter if you have the data.

## Hardware

You'll want at least 8GB of RAM (16GB is better) and about 10GB of free disk space.

## License

[![Creative Commons License](https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-nc-sa/4.0/)

This work is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-nc-sa/4.0/).
