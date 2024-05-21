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
This tool is a command-line utility designed as a wrapper around the ChNet package that can do differential network analysis by simultaneously analyzing differential gene interaction and differential gene expression. This helps to detect notable variations in gene correlation between various biological states, providing a deeper understanding of gene regulatory processes.

## Reference
For detailed methodology and application, please refer to:
Jia-Juan Tu, Le Ou-Yang, Yuan Zhu, Hong Yan, Hong Qin, Xiao-Fei Zhang, Differential network analysis by simultaneously considering changes in gene interactions and gene expression, Bioinformatics, Volume 37, Issue 23, December 2021, Pages 4414–4423, https://doi.org/10.1093/bioinformatics/btab502.


## Installation Software
Download and install the software below
 - Install RStudio
 - Install Docker
   
## Installation Instructions
Clone and navigate to the project (dgca-tool) root directory.
   ```bash
   git clone git@github.com:bionetslab/grn-benchmark.git && cd grn-benchmark/src/dgca-cli-tool
   ```
You can run the project in two ways.
- Docker
- Rscript Command Line
- 
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

## Running Locally (Using R)
 According to the [chNet](https://github.com/Zhangxf-ccnu/chNet) R package on GitHub, it should be installed as below.
```R
# Step 1. Install the devtools package. Invoke R and then type
install.packages("devtools") 

# Step 2. Load the devtools package.
library("devtools") 

# Step 3. Install the chNet package from GitHub.
install_github("Zhangxf-ccnu/chNet", subdir="pkg")
```

Execute the Chnet analysis using Rscript directly for reference gene and paper gene datasets as follows:
**500 Genes:**
```bash
Rscript Reference_data_Input_output.R --input1 "ref_dataset/500/out_CD8_exhausted.tsv" --input2 "ref_dataset/500/out_Macrophages.tsv" --output_path "Results/TSV_files/500" --file_name_suffix "500"
```
**1000 Genes:**
```bash
Rscript Reference_data_Input_output.R --input1 "ref_dataset/1000/out_CD8_exhausted.tsv" --input2 "ref_dataset/1000/out_Macrophages.tsv" --output_path "Results/TSV_files/1000" --file_name_suffix "1000"
```
**2500 Genes:**
```bash
Rscript Reference_data_Input_output.R --input1 "ref_dataset/2500/out_CD8_exhausted.tsv" --input2 "ref_dataset/2500/out_Macrophages.tsv" --output_path "Results/TSV_files/2500" --file_name_suffix "2500"
```
**TCGA.BRCA Genes:**
```bash
 Rscript TCGA.BRCA_TSV.R --dataset "TCGA.BRCA" --output_path "Results/TSV_files/paper"
```

**GSE13159.AML Genes:**
```bash
 Rscript GSE13159.AML_TSV.R --dataset "GSE13159.AML" --output_path "Results/TSV_files/paper"
```


Execute the Chnet analysis using Rscript directly for downstream analysis as follows:

**500 Genes:**
```bash
Rscript downstream_analysis.R --operation_type "ref" --input1 "ref_dataset/500/out_CD8_exhausted.tsv" --input2 "ref_dataset/500//out_Macrophages.tsv" --condition1 "CD8 Exhausted T-cells" --condition2 "Macrophages" --output_path "Results/downstream/500" --pdf_name_suffix "500"
```

**1000 Genes:**
```bash
Rscript downstream_analysis.R --operation_type "ref" --input1 "ref_dataset/1000/out_CD8_exhausted.tsv" --input2 "ref_dataset/1000//out_Macrophages.tsv" --condition1 "CD8 Exhausted T-cells" --condition2 "Macrophages" --output_path "Results/downstream/1000" --pdf_name_suffix "1000"
```
**2500 Genes:**
```bash
Rscript downstream_analysis.R --operation_type "ref" --input1 "ref_dataset/2500/out_CD8_exhausted.tsv" --input2 "ref_dataset/2500//out_Macrophages.tsv" --condition1 "CD8 Exhausted T-cells" --condition2 "Macrophages" --output_path "Results/downstream/2500" --pdf_name_suffix "2500"
```
**TCGA.BRCA Genes:**
```bash
Rscript downstream_analysis.R --operation_type "paper" --input1 "TCGA.BRCA" --condition1 "Basal" --condition2 "LumA" --output_path "Results/downstream/paper" --pdf_name_suffix "TCGA.BRCA"
```

**GSE13159.AML Genes:**
```bash
 Rscript downstream_analysis.R --operation_type "paper" --input1 "GSE13159.AML" --condition1 "cancer" --condition2 "normal" --output_path "Results/downstream/paper" --pdf_name_suffix "GSE13159.AML"
```
Replicate the Chnet paper analysis using Rscript directly for as follows:

**TCGA.BRCA Genes:**
```bash
 Rscript replicate_paper.R --input1 "TCGA.BRCA" --condition1 "Basal" --condition2 "LumA" --output_path "Results/replicate_paper" --pdf_name_suffix "TCGA.BRCA"
```

**GSE13159.AML Genes:**
```bash
 Rscript replicate_paper.R --input1 "GSE13159.AML" --condition1 "cancer" --condition2 "normal" --output_path "Results/replicate_paper" --pdf_name_suffix "GSE13159.AML"
```


4. # Make the R scripts executable
RUN chmod +x C:/Users/Piyal/Desktop/Bio/R/Docker/downstream_analysis.R
RUN chmod +x C:/Users/Piyal/Desktop/Bio/R/Docker/GSE13159.AML_TSV.R    
RUN chmod +x C:/Users/Piyal/Desktop/Bio/R/Docker/Reference_data_Input_output.R
RUN chmod +x C:/Users/Piyal/Desktop/Bio/R/Docker/replicate_paper.R 
RUN chmod +x C:/Users/Piyal/Desktop/Bio/R/Docker/TCGA.BRCA_TSV.R


   ```
<br>

## Output
- ### Input/Output Analysis
* `network.tsv`: tab-separated file that contains all edges (row-wise) with the following columns:
     * First column `target`: Target of the edge
     * Second column `regulator`: Source of the edge
     * Third column `condition`: Whether `Differential` or `Non-differential`.
     * Fourth column `weight`: Weight of the edge.

 
<br>
## Parameters
- `--input_file_1`: Path to the TSV file containing gene expression data for the first condition.
- `--input_file_2`: Path to the TSV file containing gene expression data for the second condition.
- `--output_path`: Output path where the results will be saved. The results file will be named 'network.tsv'.

## Input File Format
The input files should be TSV (Tab-Separated Values) format containing gene expression data. Each file must have genes as rows and samples as columns for each condition.

## Output File Format
| Target  | Regulator | Condition        | Weight     |
|---------|-----------|--------------    |------------|
| CLCA2  | BAMBI      | non-differential | 1          | 
| DAPL1  | SHC4       | differential     | 1          | 

**Column Descriptions:**
- **Target**: Target node of the edge.
- **Regulator**: Source node of the edge.
- **Weight**: Correlation coefficient of the gene pair for the specified condition.
- **Condition**: is it differential or non-differential
