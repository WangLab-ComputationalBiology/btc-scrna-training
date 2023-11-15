# Malignant meta-programs

## Motivation

Meta-program analyses are powerful strategies for uncovering intratumor heterogeneity (ITH). We built our meta-program module based on data published by Gavish et al. These meta-programs encompass a range of cellular processes, covering both generic patterns (such as cell cycle and stress) and cancer lineage-specific ones, e.g., 11 ITH hallmarks.

## Step-by-Step

### 1. Running pipeline

#### 1.1. On the HPC

!!! info "HPC"

    * `workflow_level`            = Malignant
    * `input_meta_programs_db`    = ./assets/meta_programs_database.csv
    * `input_cell_category`       = Malignant
    * `input_heatmap_annotation`  = source_name;seurat_clusters

```{.bash .copy}

nextflow run main.nf --workflow_level Malignant --project_name Training --sample_csv sample_table.csv --meta_data meta_data.csv --cancer_type Ovarian -resume -profile seadragon

```

#### 1.2. On Cirro

Alternatively, we execute this task on [Cirro](https://cirro.bio).

!!! info "Cirro"

    * `Defining the pipeline entrypoints`                           = Malignant
    * `Input meta-program`                                          = Default
    * `Meta-program cell category`                                  = Malignant
    * `Meta-data columns to be displayed on heatmap`                = source_name;seurat_clusters

On Cirro, users should (**Do not run**):

* Navigate to the Pipelines tab and enter "BTC scRNA Pipeline" in the search engine.
* Change the `Dataset` to **BTC Training dataset** and the `Copy Parameters From option` to **Run_01**.
* Double-check the aforementioned parameters and click **Run**.

### 2. Inspecting report

For convenience the figures can be located in the `Test_Malignant_meta_report.html` report within the **Run_02** dataset.

!!! info

    The database for **meta-programs** is stored in the pipeline repository. You can access it [here](https://github.com/break-through-cancer/btc-scrna-pipeline/blob/main/assets/cell_markers_database.csv).

#### 2.1. Meta-program and ITH prediction

The heatmap offers a detailed overview of meta-programs associated with malignant cells. Moreover, users have the option to include annotations related to meta-data, such as **source_name** and **seurat_clusters**.

![Image caption](figures/heatmap-meta-programs.png){align=center}

#### 2.2. ITH signatures

Similar to the cell annotation module, we also offer a FeaturePlot panel that reports the Module score for each ITH meta-program across malignant cells.

![Image caption](figures/featureplot-meta-program.png){align=center}

### 3. Exercise: Customizing the meta-program annotation

!!! note "Question"

    Considering meta-data for this dataset, is it possible to add or remove annotations on the heatmap? A: `Run_Meta`

**Please note:** When configuring the pipeline on Cirro, ensure that the `Dataset` is set to **BTC Training dataset** and select **Run_02** for the `Copy Parameters From option`. Additionally, configure the `Entrypoint parameter` to **Malignant**.

*Tip: Accelerate the process by skipping DEG analysis*

## Reference

1. [Hallmarks of transcriptional intratumour heterogeneity across a thousand tumours](https://www.nature.com/articles/s41586-023-06130-4)
