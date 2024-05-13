# ChNet-Tool

# Differential network analysis (ChNet) Tool

<details>
<summary>Table of Contents</summary>

- [Brief Description](#brief-description)
- [Reference](#reference)
- [Available Commands](#available-commands)
- [Installation Instructions](#installation-instructions)
  - [Using Docker](#using-docker)
- [Parameters](#parameters)
- [Input File Format](#input-file-format)
- [Output File Format](#output-file-format)

</details>

## Brief Description
This tool is a command-line utility designed as a wrapper around the ChNet package, facilitating considering changes in gene interactions and gene expression. This helps to detect notable variations in gene correlation between various biological states, providing deeper understanding of gene regulatory processes.

## Reference
For detailed methodology and application, please refer to:
Jia-Juan Tu, Le Ou-Yang, Yuan Zhu, Hong Yan, Hong Qin, Xiao-Fei Zhang, Differential network analysis by simultaneously considering changes in gene interactions and gene expression, Bioinformatics, Volume 37, Issue 23, December 2021, Pages 4414–4423, https://doi.org/10.1093/bioinformatics/btab502.

## Available Commands
The CLI includes commands for:
- Differential Correlation Analysis (ChNet)
- [Enrichment Map (enrichment_map.R)](downstream_analysis/enrichment-map.md)

In this readme, we will see the usage of dgca.R

## Installation Instructions

### Using Docker
To run the tool using Docker, ensure Docker is installed on your system and follow these steps:

1. Navigate to the project (ChNet-tool) root directory.

2. Build the Docker image:
   ```bash
   docker build -t ChNet-tool .
   ```
3. Run the tool using the Docker container:
   ```bash
   docker run --rm -v ./data:/data dgca-tool dgca.R --input_file_1 /data/BRCA_normal.tsv --input_file_2 /data/BRCA_tumor.tsv --output_path /data
   ```

## Parameters
- `--input_file_1`: Path to the TSV file containing gene expression data for the first condition.
- `--input_file_2`: Path to the TSV file containing gene expression data for the second condition.
- `--output_path`: Output path where the results will be saved. The results file will be named 'network.tsv'.

## Input File Format
The input files should be TSV (Tab-Separated Values) format containing gene expression data. Each file must have genes as rows and samples as columns for each condition.

## Output File Format
| Target  | Regulator | Condition        | Weight        |
|---------|-----------|--------------    |---------------|
| CLCA2  | BAMBI      | non-differential | -0.070261455  | 
| DAPL1  | SHC4       | differential     | 0.9567267     | 

**Column Descriptions:**
- **Target**: Target node of the edge.
- **Regulator**: Source node of the edge.
- **Weight**: Correlation coefficient of the gene pair for the specified condition.
- **Condition**: is it differential or non-differential
