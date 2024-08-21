# HTS-PROJECT

Single variant genotyping is a critical technique in genomics that focuses on identifying and characterizing single nucleotide variants (SNVs) within the genome. SNVs are the most common form of genetic variation among individuals, playing a significant role in genetic diversity, disease susceptibility, and personalized medicine. The genotyping process typically involves sample preparation, high-throughput sequencing (HTS), data processing, variant calling, and annotation. By employing advanced algorithms, researchers can distinguish true variants from sequencing errors, providing insights into their potential biological significance and associations with various diseases.

The applications of single variant genotyping are vast, ranging from clinical research and population genetics to agricultural genomics. It enables the identification of genetic markers linked to diseases, facilitating improved diagnostics and targeted therapies. However, challenges such as data complexity, the risk of false positives, and ethical considerations regarding genetic testing must be addressed. As genomic technologies continue to evolve, single variant genotyping remains a powerful tool for advancing our understanding of genetics and its implications for health and disease.

This is a project using high throughput sequencing technology for single variable genotyping.

#The Work Environment

This project took place in a Linux Environment.

# Dataset

The dataset used in this project was human sequencing data. The following links were put in Linux to get the data.

```

https://zenodo.org/record/3243160/files/father_R1.fq.gz
https://zenodo.org/record/3243160/files/father_R2.fq.gz
https://zenodo.org/record/3243160/files/mother_R1.fq.gz
https://zenodo.org/record/3243160/files/mother_R2.fq.gz
https://zenodo.org/record/3243160/files/proband_R1.fq.gz
https://zenodo.org/record/3243160/files/proband_R2.fq.gz

```

The dataset includes sequencing data of a family or 3, which includes the father, mother and a child.

# Reference Genome

The reference genome used in this project was gotten in Linux using the link below

```
https://zenodo.org/record/3243160/files/hg19_chr8.fa.gz
```
# Quality Check

After sourcing the data, the next step was to do a quality check on the data using FastQC in Linux Environment. 
The code used to do this was 



