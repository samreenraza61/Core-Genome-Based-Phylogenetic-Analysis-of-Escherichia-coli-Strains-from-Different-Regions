# Core Genome-Based Phylogenetic Analysis of *Escherichia coli* Strains from Different Regions

## 🔍 Research Question / Objective
**"How do different strains of *Escherichia coli* (E. coli) from various geographical regions cluster based on their core genome sequences, and what does this reveal about their evolutionary relationship?"**

---

## 📥 Genome Data Collection

Five complete genomes of *E. coli* strains were downloaded from the [NCBI Genome database](https://www.ncbi.nlm.nih.gov/genome/). The selected strains represent diverse geographic regions.

| # | Strain Name              | Assembly Accession     | Region |
|---|--------------------------|------------------------|--------|
| 1 | K-12 MG1655              | GCF_000005845.2        | USA    |
| 2 | O157:H7 Sakai            | GCF_000008865.2        | Japan  |
| 3 | UTI89                    | GCF_000013265.1        | USA    |
| 4 | 14EC020                  | GCF_002853715.1        | China  |
| 5 | DSM 30083 (ATCC 11775)   | GCF_003697165.2        | USA    |

**Downloaded File Format**: `.fna` (nucleotide FASTA format)

---

## 🧪 Step-by-Step Workflow

### 1️⃣ Genome Annotation  
- **Tool Used**: [Prokka](https://github.com/tseemann/prokka)  
- **Platform**: [Galaxy Europe](https://usegalaxy.eu/)

Each genome was annotated using Prokka to identify genes and generate GFF files required for core genome analysis.

**Input**: `.fna` genome files  
**Output**: `.gff` annotation files (used in core genome analysis)

---

### 2️⃣ Core Genome Analysis  
- **Tool Used**: [Roary](https://sanger-pathogens.github.io/Roary/)  
- **Platform**: [Galaxy Europe](https://usegalaxy.eu/)

Roary was used to compute the core and accessory genome. It aligns the annotated .gff files and identifies shared genes.

**Input**: All `.gff` files generated from Prokka  
**Outputs**:
- `core_gene_alignment.aln` – Multiple sequence alignment of core genes  
- `gene_presence_absence.csv` – Matrix of gene distribution  
- Summary statistics (core, accessory, shell genes)

---

### 3️⃣ Phylogenetic Tree Construction  
- **Tool Used**: [FastTree](http://www.microbesonline.org/fasttree/)  
- **Platform**: [Galaxy Europe](https://usegalaxy.eu/)

Constructed an approximately maximum-likelihood phylogenetic tree based on the aligned core genome.

**Input**: `core_gene_alignment.aln`  
**Output**: Newick format tree file (`*.nwk`)

---

### 4️⃣ Phylogenetic Tree Visualization  
- **Tool Used**: [iTOL (Interactive Tree of Life)](https://itol.embl.de/)

Used iTOL to upload and annotate the .nwk tree with metadata such as strain names and geographic origin.

**Inputs**:
- `.nwk` tree file  
- Metadata file for annotation:

**Outputs**:
- Interactive phylogenetic tree with colored clades by region or strain type

---

## 🧰 Summary of Tools Used

| Task                         | Tool/Software       | Access Platform           |
|------------------------------|---------------------|----------------------------|
| Genome annotation            | Prokka              | [Galaxy Europe](https://usegalaxy.eu/) |
| Core genome analysis         | Roary               | [Galaxy Europe](https://usegalaxy.eu/) |
| Alignment & Tree construction| Roary + FastTree    | [Galaxy Europe](https://usegalaxy.eu/) |
| Visualization                | iTOL                | [iTOL Web](https://itol.embl.de/) |

---

## 🧪 Results and Conclusion

### 1️⃣ Phylogenetic Tree Interpretation

The phylogenetic tree was constructed using the aligned core genome sequences and visualized with iTOL. Each strain was color-coded according to its geographical region:

| Strain ID                                      | Region | Color   |
|------------------------------------------------|--------|---------|
| Prokka_on_GCF_000008865.2_ASM886v2             | Japan  | Orange  |
| Prokka_on_GCF_000005845.2_ASM584v2             | USA    | Teal    |
| Prokka_on_GCF_002853715.1_ASM285371v1          | China  | Green   |
| Prokka_on_GCF_003697165.2_ASM369716v2          | USA    | Pink    |
| Prokka_on_GCF_000013265.1_ASM1326v1            | USA    | Purple  |

**Clustering Observations**:
- Two USA strains (**ASM1326v1** and **ASM369716v2**) clustered closely within the same clade, suggesting a closer evolutionary relationship.
- The third USA strain (**ASM584v2**) was distantly placed from the other two, indicating notable genomic variation even within strains from the same country.
- The Japan strain (**ASM886v2**) branched off earlier than all others, forming an isolated lineage.
- The China strain (**ASM285371v1**) clustered near the two USA strains (**ASM1326v1** and **ASM369716v2**), showing closer similarity to them than to the Japan or distant USA strain.

---

### 2️⃣ Core Genome Summary (`gene_presence_absence.csv`)

| Gene Category      | Count |
|--------------------|-------|
| Core genes (100%)  | 2     |
| Soft core (95–99%) | 0     |
| Shell genes (15–95%)| 6,202 |
| Cloud genes (<15%) | 0     |

**Interpretation**:
- Only **2 core genes** were present across all five strains, indicating a very low level of universally shared genes.
- A total of **6,202 shell genes** were found, representing genes shared by some but not all strains.
- No soft core or cloud genes were detected in this dataset.

These findings indicate that the selected *E. coli* strains exhibit **high genomic variability**, with very few genes conserved across all samples.

---

### 🔍 Overall Conclusion

The results suggest that *Escherichia coli* strains cluster partially based on geographical origin. Two of the three USA strains formed a close clade, whereas the third USA strain diverged significantly. The Japan strain formed a separate early-branching lineage, and the China strain clustered near two USA strains.

Additionally, the presence of only two core genes and thousands of shell genes indicates substantial diversity among the selected genomes. These observations reflect strain-specific differences at the core genome level and suggest varying evolutionary paths among *E. coli* isolates from different regions.

---

## 📚 References

1. Seemann, T. (2014). **Prokka: rapid prokaryotic genome annotation**. *Bioinformatics*, 30(14), 2068–2069. https://doi.org/10.1093/bioinformatics/btu153  
2. Page, A. J., et al. (2015). **Roary: rapid large-scale prokaryote pan genome analysis**. *Bioinformatics*, 31(22), 3691–3693. https://doi.org/10.1093/bioinformatics/btv421  
3. Price, M. N., Dehal, P. S., & Arkin, A. P. (2010). **FastTree 2 – Approximately Maximum-Likelihood Trees for Large Alignments**. *PLoS ONE*, 5(3), e9490. https://doi.org/10.1371/journal.pone.0009490  
4. Letunic, I., & Bork, P. (2021). **Interactive Tree Of Life (iTOL) v5**. *Nucleic Acids Research*, 49(W1), W293–W296. https://doi.org/10.1093/nar/gkab301

---

## ⚠️ Disclaimer

> **This project is conducted solely for learning purposes and is not intended for publication or clinical research.**
