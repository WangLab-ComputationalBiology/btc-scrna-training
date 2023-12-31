# Cell-cell communication

## Motivation

Cell-cell communication analysis offers insights into the interactions among different cell types within a tissue or tumor. These interactions form intricate networks that can reveal mechanisms associated with alterations in the tumor microenvironment and disease progression. To decipher this complex orchestration, we utilize well-established methods from the literature, specifically **CellChat** and **LIANA**.

## Step-by-step

### 1. Running pipeline

#### 1.1. On HPC

!!! info "HPC"

    * `workflow_level`              = nonMalignant
    * `input_source_groups`         = all
    * `input_target_groups`         = all
    * `input_cellchat_annotation`   = Secreted Signaling

```{.bash .copy}

nextflow run main.nf --workflow_level nonMalignant --project_name Training --sample_csv sample_table.csv --meta_data meta_data.csv --cancer_type Ovarian -resume -profile seadragon

```

#### 1.2. On Cirro

Alternatively, we execute this task on [Cirro](https://cirro.bio).

!!! info "Cirro"

    * `Defining the pipeline entrypoint`    = nonMalignant
    * `Source cell type names`              = all
    * `Target cell type names`              = all
    * `CellChat interactions type`          = Secreted Signaling

On Cirro, users should (**Do not run**):

* Navigate to the Pipelines tab and enter "BTC scRNA Pipeline" in the search engine.
* Change the `Dataset` to **BTC Training dataset** and the `Copy Parameters From option` to **Run_01**.
* Double-check the aforementioned parameters and click **Run**.

### 2. Inspecting report

For convenience the figures can be located in the `Test_communication_report.html` report within the **Run_02** dataset.

#### 2.1. LIANA output

The bubble plot illustrates the interactions between ligand-receptor (L-R) pairs across various cell types, including interaction specificity and expression magnitude metrics. Interaction specificity measures the degree of L-R exclusivity among cell types, i.e., putative a preferential "communication" pathway. Meanwhile, expression magnitude indicates the strength of L-R interactions within a cell population.

![Image caption](figures/bubble-liana-communication.png){align=center}

The heatmap displays the interaction directionality between Sender and Receiver populations.

![Image caption](figures/heatmap-liana-strength.png){align=center}

#### 2.2. CellChat output

Alternatively, we can explore results obtained exclusively from CellChat. The network displays various metrics related to interaction strength and frequency across populations. These can be further divided into cell-based plots, as detailed below.

![Image caption](figures/circus-cellchat.png){align=center}

![Image caption](figures/circus-cellchat-subset.png){align=center}

### 3. Exercise: Manipulating cell-cell communication database

!!! note "Question"

    What happens when switching the interaction type to Cell-Cell Contact? A: `Run_Cell_Contact`

**Please note:** When configuring the pipeline on Cirro, ensure that the `Dataset` is set to **BTC Training dataset** and select **Run_02** for the `Copy Parameters From option`. Additionally, configure the `Entrypoint parameter` to **nonMalignant**.

*Tip: Accelerate the process by skipping DEG and Doublets analyses*

## Reference

1. [Comparison of methods and resources for cell-cell communication inference from single-cell RNA-Seq data](https://www.nature.com/articles/s41467-022-30755-0)
2. [Inference and analysis of cell-cell communication using CellChat](https://www.nature.com/articles/s41467-021-21246-9)
