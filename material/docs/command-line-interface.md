# Command-line interface

## Pipeline parameters

| Parameter | Description | Type | Default | 
|-----------|-----------|-----------|-----------|
| `workflow_level` | Entrypoint parameter | `string` | Complete |

## Project parameters

| Parameter | Description | Type | Default | 
|-----------|-----------|-----------|-----------|
| `sample_table` | Path to sample table | `string` | ./assets/test_sample_table.csv |
| `meta_data` | Path to meta-data | `string` | ./assets/test_meta_data.csv |
| `project_name` | Project name | `string` | Test |
| `cancer_type` | Enter the cancer type | `string` | None |
| `genome` | Enter genome name | `string` | GRCh38 |
| `igenomes_base` | Enter URL/Path to the genome | `string` | gs://btc-refdata/scRNA/refData |

## Quality Control parameters

| Parameter | Description | Type | Default | 
|-----------|-----------|-----------|-----------|
| `thr_estimate_n_cells` | Estimated number of cells | `integer` | 300 |
| `thr_mean_reads_per_cells` | Mean reads per cell | `integer` | 25000 |
| `thr_median_genes_per_cell` | Median genes per cell | `integer` | 900 |
| `thr_median_umi_per_cell` | Median UMI per cell | `integer` | 1000 |
| `thr_n_feature_rna_min` | Minimum features per cell | `integer` | 300 |
| `thr_n_feature_rna_max` | Maximum features per cell | `integer` | 7500 |
| `thr_percent_mito` | Percentage of mitochondrial genes | `integer` | 25 |
| `thr_n_observed_cells` | Number of observed cells | `integer` | 300 |

## Normalization parameters

| Parameter | Description | Type | Default | 
|-----------|-----------|-----------|-----------|
| `thr_n_features` | Number features for FindVariableFeatures | `integer` | 2000 |

## Clustering parameters

| Parameter | Description | Type | Default | 
|-----------|-----------|-----------|-----------|
| `input_features_plot` | Genes to be displayed on Feature plot | `string` | LYZ;CCL5;IL32;PTPRCAP;FCGR3A;PF4;PTPRC |
| `input_integration_dimension` | Embeddings for Louvain clustering | `string` | auto |
| `input_group_plot` | Meta-data columns for UMAP plot | `string` | source_name;Sort |
| `thr_resolution` | Resolution threshold | `number` | 0.25 |
| `thr_proportion` | Cell proportion for ROGUE calculation | `number` | 0.25 |

## Stratification parameters

| Parameter | Description | Type | Default | 
|-----------|-----------|-----------|-----------|
| `input_stratification_method` | Method to define stratification labels | `string` | infercnv_label |
| `thr_cluster_size` | Defining cluster size limit | `integer` | 1000 |
| `thr_consensus_score` | Consensus score threshold (Beta) | `integer` | 2 |

## Cell annotations parameters

| Parameter | Description | Type | Default | 
|-----------|-----------|-----------|-----------|
| `input_cell_markers_db` | Path to cell annotation CSV file | `string` | ./assets/cell_markers_database.csv |
| `input_annotation_level` | Define annotation level. Currently, only Major cells are available. | `string` | Major cells |

## Cell-cell communication parameters

| Parameter | Description | Type | Default | 
|-----------|-----------|-----------|-----------|
| `input_source_groups` | Source cell type names | `string` | all |
| `input_target_groups` | Target cell type names | `string` | all |
| `input_cellchat_annotation` | CellChat interactions type | `string` | Secreted Signaling |


## Batch correction parameters

| Parameter | Description | Type | Default | 
|-----------|-----------|-----------|-----------|
| `input_integration_method` | Batch correction / Integration methods. Default (all). | `string` | all |
| `input_target_variables` | Meta-data target variable for batch correction | `string` | batch |

## Batch Evaluation parameters

| Parameter | Description | Type | Default | 
|-----------|-----------|-----------|-----------|
| `input_integration_evaluate` | Define methods to be evaluated | `string` | all |
| `thr_cell_proportion` | Cell proportion for Batch evaluation | `number` | 0.3 |
| `input_lisi_variables` | Define LISI types for Density plot | `string` | cLISI;iLISI |

## Differential Expression parameters

| Parameter | Description | Type | Default | 
|-----------|-----------|-----------|-----------|
| `input_deg_method` | Define DEG method (check options at Seurat documentation) | `string` | wilcox |
| `input_top_deg` | Number of DEG to be displayed | `integer` | 20 |
| `thr_fold_change` | Fold-change threshold | `number` | 0.25 |
| `thr_min_percentage` | Minimum cell percentage per DEG | `number` | 0.1 |
| `opt_hgv_filter` | Filtering only HGV genes (Optional) | `boolean` | False |

## Meta-program parameters

| Parameter | Description | Type | Default | 
|-----------|-----------|-----------|-----------|
| `input_meta_programs_db` | Path to meta-program CSV file | `string` | ./assets/meta_programs_database.csv |
| `input_cell_category` | Meta-program cell category | `string` | Malignant |
| `input_heatmap_annotation` | Meta-data columns to be displayed on heatmap | `string` | source_name;seurat_clusters |
