# Getting started

## Installation

### 1. Nextflow and third-party software

Nextflow can be used on any POSIX-compatible system (Linux, OS X, WSL). It requires Bash 3.2 (or later) and Java 11 (or later, up to 18) to be installed.

```{ .bash .copy }
wget -qO- https://get.nextflow.io | bash
```

### 2. Containerization

In line with contemporary pipelines, the BTC scRNA pipeline is powered by multiple Docker container. On that note, distinct computational environments will depend on distinct container technologies, such as Docker (v20.10.22) and Singularity (v3.7.0). For instance, HPC strongly depend on Singularity, therefore it should be explicited defined into `profile` configurations. For a better understanding, refer to the [advanced](advanced.md) section. Additionally, check the [containers](https://github.com/break-through-cancer/btc-sc-containers) repository.

### 3. Cloning scRNA-Seq Pipeline

```{ .bash .copy }
git clone https://github.com/WangLab-ComputationalBiology/btc-scrna-pipeline
```
### 4. Running single-cell pipeline

The pipeline requires four parameters: `project name`, `sample_table`, `meta_data`, `cancer_type` . In particular, sample_table and meta_data should follow a **mandatory** format as described below.

#### 4.1. Preparing inputs

The sample table must be a CSV file containing four columns: sample, fastq_1, and fastq_2. The sample column will be linked to all reports generated by the pipeline. Additionally, it's essential for merging the metadata with the Seurat object. **Example** [sample sheet](./assets/ovarian_sample_table.csv){:download="ovarian_sample_table.csv"}.

{{ read_csv('./assets/ovarian_sample_table.csv') }}

The metadata file, in .csv format, should encompass variables pertinent to the experimental design, such as batch and cell sorting status. It can also include additional biological information about the sample. The batch variable is utilized to correct effects. In this version of the pipeline, correction is based on a singular variable. **Example** [meta-data](./assets/ovarian_meta_data.csv){:download="ovarian_meta_data.csv"}.

{{ read_csv('./assets/ovarian_meta_data.csv') }}

!!! warning

    Internally, the pipeline expects the batch column. This column will be used to perform the batch correction approach.

#### 4.2. Minimal command-line

To execute the pipeline, users should use the command line structure outlined below. **Please**, note the semantic differences between using one dash (-) for Nextflow commands and two dashes (--) for pipeline commands. Commands with two dashes are just for specific pipeline tasks, like adjusting filtering or thresholds on the single-cell analysis.

```{ .bash .copy }
nextflow run single_cell_basic.nf --project_name <PROJECT> --sample_csv <path/to/sample_table.csv> --meta_data <path/to/meta_data.csv> --cancer_type <CANCER TYPE> -resume -profile <PROFILE>
```
At the end, the pipeline will make a folder named after the `--project_name` command. This folder will have all the results. The `-resume` command leverage Nextflow caching, i.e., resuming executions to avoid undesirable computational time.

#### 4.3. Staging images and genome indexes

The pipeline needs to stage (download) multiple components to run. This can pose challenges in HPC environments with strict network policies. As a solution, consider using the `-stub` option on a node with a network connection. The `-stub` will stage all the necessary components without actually executing any analysis. Thus, it serves as a bootstrap run for the pipeline. Please note that **stub** will generate dummy outputs.

```{ .bash .copy }
nextflow run single_cell_basic.nf --project_name <PROJECT> --sample_csv <path/to/sample_table.csv> --meta_data <path/to/meta_data.csv> --cancer_type <CANCER TYPE> -resume -profile <PROFILE> -stub
```
#### 4.4. Shorten command-line

Long command lines can be tricky. Thankfully, with Nextflow's `-params-file`, we can make things simpler. This is a JSON file that has all the instructions related to a specific run. If you're trying out different settings, it could a best practices to keep separate files for each test, e.g., PARAMS_TEST_01.json or PARAMS_TEST_02.json.

```{ .bash .copy }
{
 "project_name": "BTC-CANCER-X",
 "sample_csv": "path/to/sample_table.csv",
 "meta_data": "path/to/meta_data.csv",
 "cancer_type": "CANCER TYPE X"
 "thr_mean_reads_per_cells": 10000
}
```

Note, other paramaters can be added into the `-params-file`. 

```{ .bash .copy }
nextflow run single_cell_basic.nf -params-file <PARAMS.json> -resume -profile <PROFILE>
```

### 5. Expect outputs

![Image caption](figures/schema-output.png){align=center}
