# Cell stratification and CNV

## Motivation

Distinguishing malignant cells from normal cells remains a significant challenge in single-cell transcriptomics. To confidently identify malignant cells among other cell populations, multiple pieces of evidence are necessary. In our pipeline, we have incorporated two common types of evidence: gene signatures and CNV analysis.

## Step-by-step

In this module, we employ a conservative strategy, offering users the choice between two distinct methods for identifying malignant populations: i) the inferCNV-based method, and ii) the consensus score. The consensus score is a method currently under development, which amalgamates gene signatures, various CNV predictions, and cluster/patient specificity.

### 1. Running pipeline

#### 1.1. On the HPC

By default the previous command line considers thresholds.

!!! info "HPC"

    * `workflow_level`                          = Stratification
    * `input_stratification_method`             = infercnv_label
    * `thr_cluster_size`                        = 1000
    * `thr_consensus_score`                     = 2

```{.bash .copy}

nextflow run single_cell_basic.nf --workflow_level Stratification --project_name Training --sample_csv sample_table.csv --meta_data meta_data.csv --cancer_type Ovarian -resume -profile seadragon

```

#### 1.2. On Cirro

Alternatively, we execute this task on [Cirro](https://cirro.bio).

!!! info "Cirro"

    * `Defining the pipeline entrypoints`                 = Stratification
    * `Method to define stratification labels`            = infercnv_label
    * `Defining cluster size limit`                       = 1000
    * `Consensus score threshold (Beta)`                  = 2

On Cirro, users should (**Do not run**):

* Navigate to the Pipelines tab and enter "BTC scRNA Pipeline" in the search engine.
* Change the `Dataset` to **BTC Training dataset** and the `Copy Parameters From option` to **Run_01**.
* Double-check the aforementioned parameters and click **Run**.

### 2. Inspecting report

For convenience the figures can be located in the `Test_stratification_report.html` report within the **Run_02** dataset.

#### 2.1. InferCNV predictions

The first UMAP displays malignancy status based on inferCNV predictions. By default, the pipeline will utilize this annotation for downstream analysis. The inferCNV utilizes a time-consuming statistical method, therefore we applied a heuristic approach by subsampling cells per cluster, `thr_cluster_size`. In summary, the method performs well, but it has limitations in displaying misassigned cells, and low accuracy in small populations.

![Image caption](figures/umap-infercnv.png){align=center}

!!! warning

    InferCNV predictions are carried out in two distinct modes: reference-based, which leverages known malignant cells from the single-cell experiment, and reference-free mode, which employs a statistical procedure to estimate the CNV load cut-off. Currently, we utilize the reference-free mode. **The pipeline stores the inferCNV heatmap in the data folder**.

#### 2.2. Consensus approach (under development)

Alternatively, we also offer annotations based on the consensus approach (**under development**), which appears to more effectively capture smaller cell populations. However, neither approach can be considered flawless.

![Image caption](figures/umap-consensus.png){align=center}

!!! info

    The user can change malignancy classifier by switching the parameter, `input_stratification_method`. The options are **infercnv_label** or **consensus_label**.

#### 2.3. CD45 marker based on FACS

![Image caption](figures/umap-cd45.png){align=center}

The malignancy prediction can generally be correlated with CD45 status (protein-level expression). However, minor discrepancies might be linked to the presence of **normal** epithelial cells in the dataset.

### 3. Exercise: Exploring alternative approaches to perform malignant identification

!!! note "Question"

    Does the consensus method affect the meta-program analysis? What happens if we change the consensus threshold? A: `Run_Consensus` and `Run_Consensus_Meta_Threshold`

**Please note:** When configuring the pipeline on Cirro, ensure that the `Dataset` is set to **BTC Training dataset** and select **Run_02** for the `Copy Parameters From option`. Additionally, configure the `Entrypoint parameter` to **Stratification**.

*Tip: Accelerate the process by reducing cluster size limit to 100*

## Reference

1. [Infer Copy Number Variation from Single-Cell RNA-Seq Data](https://bioconductor.org/packages/release/bioc/html/infercnv.html)