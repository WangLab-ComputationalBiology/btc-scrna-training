# Malignant meta-programs

## Motivation

Meta-program analyses are powerful strategies for uncovering intratumor heterogeneity (ITH). We built our meta-program module based on data published by Gavish et al. These meta-programs encompass a range of cellular processes, covering both generic patterns (such as cell cycle and stress) and cancer lineage-specific ones, e.g., 11 ITH hallmarks.

## Step-by-Step

### 1. Running pipeline

#### 1.1. On the HPC

!!! info "HPC"

    * `input_meta_programs_db`    = ./assets/meta_programs_database.csv
    * `input_cell_category`       = Malignant
    * `input_heatmap_annotation`  = source_name;seurat_clusters

```{.bash .copy}

nextflow run single_cell_basic.nf --project_name Training --sample_csv sample_table.csv --meta_data meta_data.csv --cancer_type Ovarian -resume -profile seadragon

```

#### 1.2. On Cirro

Alternatively, we execute this task on [Cirro](https://cirro.bio).

!!! info "Cirro"

    * `Input meta-program`                                          = Default
    * `Meta-program cell category`                                  = Malignant
    * `Meta-data columns to be displayed on heatmap`                = source_name;seurat_clusters

**Please note:** When setting up the pipeline form make sure the `Dataset` is configured to **BTC Training dataset** and choose **Run_01** for the `Copy Parameters From option`. Additionally, set the `Entrypoint parameter` to **Complete**.

### 2. Inspecting report

For your reference, the figures we are discussing are located in the `Test_Malignant_meta_report.html` report. You can find this report inside the **Run_02** folder.

#### 2.1. Meta-program and ITH prediction

The heatmap offers a detailed overview of meta-programs associated with malignant cells. Moreover, users have the option to include annotations related to meta-data, such as **source_name** and **seurat_clusters**.

![Image caption](figures/heatmap-meta-programs.png){align=center}

#### 2.2. ITH signatures

Similar to the cell annotation module, we also offer a FeaturePlot panel that reports the Module score for each ITH meta-program across malignant cells.

![Image caption](figures/featureplot-meta-program.png){align=center}

### 3. Exercise: Customizing the meta-program annotation

!!! note "Question"

    Considering meta-data for this dataset, is it possible to add or remove annotations on the heatmap?


## Reference

1. [Hallmarks of transcriptional intratumour heterogeneity across a thousand tumours](https://www.nature.com/articles/s41586-023-06130-4)