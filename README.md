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



# **HIGHTHROUGHPUT PROJECT DETAILS**

## **Step 1: Downloading the Datasets**

### **Father Dataset**
```bash
wget https://zenodo.org/record/3243160/files/father_R1.fq.gz
wget https://zenodo.org/record/3243160/files/father_R2.fq.gz
```
### **Mother Dataset**
```bash
wget https://zenodo.org/record/3243160/files/mother_R1.fq.gz
wget https://zenodo.org/record/3243160/files/mother_R2.fq.gz
```
### **Child Dataset (Proband)**
```bash
wget https://zenodo.org/record/3243160/files/proband_R1.fq.gz
wget https://zenodo.org/record/3243160/files/proband_R2.fq.gz
```

---

## **Step 2: Downloading the hg19 Reference Genome**
```bash
wget https://zenodo.org/record/3243160/files/hg19_chr8.fa.gz
```

---

## **Step 3: Running FastQC on the Datasets**
```bash
fastqc father_R1.fq.gz
fastqc father_R2.fq.gz
fastqc mother_R1.fq.gz
fastqc mother_R2.fq.gz
fastqc proband_R1.fq.gz
fastqc proband_R2.fq.gz
```

---

## **Step 4: Indexing the Reference Genome**
```bash
bwa index hg19_chr8.fa.gz
```

---

## **Step 5: Read Mapping**
```bash
bwa mem -t 8 hg19_chr8.fa.gz father_R1.fq.gz father_R2.fq.gz > fatheroutput.sam
bwa mem -t 8 hg19_chr8.fa.gz mother_R1.fq.gz mother_R2.fq.gz > motheroutput.sam
bwa mem -t 8 hg19_chr8.fa.gz proband_R1.fq.gz proband_R2.fq.gz > probandoutput.sam
```

---

## **Step 6: Converting SAM Files to BAM Files**
```bash
samtools view -bS fatheroutput.sam > fatheroutput.bam
samtools view -bS motheroutput.sam > motheroutput.bam
samtools view -bS probandoutput.sam > probandoutput.bam
```

---

## **Step 7: Sorting the BAM Files**
```bash
samtools sort fatheroutput.bam -o fatheroutput.sorted.bam
samtools sort motheroutput.bam -o motheroutput.sorted.bam
samtools sort probandoutput.bam -o probandoutput.sorted.bam
```

---

## **Step 8: Indexing the BAM Files**
```bash
samtools index fatheroutput.sorted.bam
samtools index motheroutput.sorted.bam
samtools index probandoutput.sorted.bam
```

---

## **Step 9: Filtering the BAM Files**
```bash
samtools view -F 4 -q 30 -b fatheroutput.sorted.bam > father_filtered.bam
samtools view -F 4 -q 30 -b motheroutput.sorted.bam > mother_filtered.bam
samtools view -F 4 -q 30 -b probandoutput.sorted.bam > proband_filtered.bam
```

---

## **Step 10: Removing Duplicate Reads**

### **Sorting BAM Files by Name**
```bash
samtools sort -n father_filtered.bam -o father_filtered.name_sorted.bam
samtools sort -n mother_filtered.bam -o mother_filtered.name_sorted.bam
samtools sort -n proband_filtered.bam -o proband_filtered.name_sorted.bam
```

### **Fixmating Sorted Files**
```bash
samtools fixmate -m father_filtered.name_sorted.bam father_fixmate.bam
samtools fixmate -m mother_filtered.name_sorted.bam mother_fixmate.bam
samtools fixmate -m proband_filtered.name_sorted.bam proband_fixmate.bam
```

### **Sorting Fixmated BAM Files by Coordinates**
```bash
samtools sort father_fixmate.bam -o father_fixmate.sorted.bam
samtools sort mother_fixmate.bam -o mother_fixmate.sorted.bam
samtools sort proband_fixmate.bam -o proband_fixmate.sorted.bam
```

### **Removing Duplicates**
```bash
samtools markdup -r father_fixmate.sorted.bam father_dedup.bam
samtools markdup -r mother_fixmate.sorted.bam mother_dedup.bam
samtools markdup -r proband_fixmate.sorted.bam proband_dedup.bam
```

---

## **Step 11: Variant Calling**

### **Indexing the Deduplicated BAM Files**
```bash
samtools index father_dedup.bam
samtools index mother_dedup.bam
samtools index proband_dedup.bam
```

### PROJECT IMAGES

# Father Dataset 
![Image](https://github.com/user-attachments/assets/b7b2f0ce-bb5a-4e23-b3de-42275b84560a)

![Image](https://github.com/user-attachments/assets/3e7f28fb-e519-4e30-90e0-c7bede2c94b3)

# Mother Dataset

![Image](https://github.com/user-attachments/assets/801bd7cd-5b31-4e01-b8a6-39138f6095bc)

# Child Dataset

![Image](https://github.com/user-attachments/assets/1b58d01d-66ad-48f9-976a-9ab7fd7d4192)

# Getting hg19 Version of the Human Dataset

![Image](https://github.com/user-attachments/assets/6ffb5e87-869a-468f-a904-c90bd9ec8065)

# Running Fastqc on the Datasets

![Image](https://github.com/user-attachments/assets/4abc3157-3e06-432f-881a-28e00f806e9f)

![Image](https://github.com/user-attachments/assets/8b4b673c-7a7e-480d-9c43-f06fe2378140)

![Image](https://github.com/user-attachments/assets/87321358-57eb-4c04-827b-dbbeb29f570c)

# Converting SAM files to BAM files

![Image](https://github.com/user-attachments/assets/403fc08d-021f-4b87-99f8-ca362bba9aa4)

# Sorting the BAM files

![Image](https://github.com/user-attachments/assets/114c6cac-62ff-4773-8cd1-06d06b0eddb8)

# Indexing the BAM files

![Image](https://github.com/user-attachments/assets/fdadcf44-0547-4022-bb95-e53692959ec7)

# Filtering the BAM Files

![Image](https://github.com/user-attachments/assets/1ccb9846-90af-490f-a687-ac7ae6359819)

# Removing Duplicate Reads

![Image](https://github.com/user-attachments/assets/e09e3705-89da-4948-be17-34891740d95a)

# Fixmate sorted files

![Image](https://github.com/user-attachments/assets/0190da7b-2d3d-4fa2-989b-0ce30a051feb)

# Sorting the fixmated bam files according to coordinates
 
![Image](https://github.com/user-attachments/assets/3b78b4e0-1e9d-4440-b88f-a449c7ba3e21)

# Removing duplicates
 ![Image](https://github.com/user-attachments/assets/0db01224-2bde-4f2b-9369-0bda541492db)

# VARIANT CALLING

![Image](https://github.com/user-attachments/assets/50df9a90-5bc4-4233-814b-235cc0be1cd2)

 






