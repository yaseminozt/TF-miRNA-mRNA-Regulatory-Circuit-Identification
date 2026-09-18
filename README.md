# TF–miRNA–mRNA Regulatory Circuit Identification

This repository contains the C source codes used for the identification of
transcription factor (TF)–miRNA–target gene regulatory circuits.

The workflow generates candidate TF–gene, miRNA–gene, miRNA–TF and TF–miRNA
pairs and subsequently identifies overlapping regulatory interactions to
construct TF–miRNA–mRNA regulatory circuits.

## Repository structure

```text
.
├── README.md
├── code/
│   ├── 01_generate_regulatory_pairs.c
│   ├── 02_identify_miRNA_gene_interactions.c
│   ├── 03_identify_miRNA_TF_interactions.c
│   ├── 04_identify_TF_gene_interactions.c
│   ├── 05_identify_TF_miRNA_interactions.c
│   ├── 06_construct_miRNA_TF_gene_triplets.c
│   └── 07_identify_TF_miRNA_gene_circuits.c
├── input/
└── output/
```

## Requirements

A standard C compiler is required. GCC can be used, for example:

```bash
gcc code/01_generate_regulatory_pairs.c -o generate_pairs
```

## Input files

The programs expect input files with the following names, depending on the
analysis step:

- `TF.txt`
- `MiRNA.txt`
- `Gene.txt`
- `MiGene_control.txt`
- `MiTF_control.txt`
- `TFGene_control.txt`
- `TFMi_control.txt`

The original programs read these files from the working directory using
relative file names. Therefore, place the required input files in the same
working directory as the executable, or adapt the file paths in the source
code.

## Analysis steps

### Step 1 — Generate candidate regulatory pairs

`01_generate_regulatory_pairs.c`

Generates all possible combinations of the supplied TF, miRNA and gene
lists for the corresponding pair types and writes them to:

- `MiGene.txt`
- `TFGene.txt`
- `MiTF.txt`
- `TFMi.txt`

### Step 2 — Identify miRNA–gene interactions

`02_identify_miRNA_gene_interactions.c`

Compares `MiGene_control.txt` with `MiGene.txt` and writes the overlapping
pairs to `ResultMiGene.txt`.

### Step 3 — Identify miRNA–TF interactions

`03_identify_miRNA_TF_interactions.c`

Compares `MiTF_control.txt` with `MiTF.txt` and writes the overlapping pairs
to `ResultMiTF.txt`.

### Step 4 — Identify TF–gene interactions

`04_identify_TF_gene_interactions.c`

Compares `TFGene_control.txt` with `TFGene.txt` and writes the overlapping
pairs to `ResultTFGene.txt`.

### Step 5 — Identify TF–miRNA interactions

`05_identify_TF_miRNA_interactions.c`

Compares `TFMi_control.txt` with `TFMi.txt` and writes the overlapping pairs
to `ResultTFMi.txt`.

### Step 6 — Construct miRNA–TF–gene triplets

`06_construct_miRNA_TF_gene_triplets.c`

Integrates the identified miRNA–gene and miRNA–TF relationships and produces
candidate miRNA–TF–gene triplets in:

`ResultMiTFGene.txt`

### Step 7 — Identify TF–miRNA–gene regulatory circuits

`07_identify_TF_miRNA_gene_circuits.c`

Further intersects the candidate triplets with TF–gene relationships and
writes the resulting regulatory circuits to:

`Result.txt`

The final refinement step uses TF–miRNA relationships to generate the final
set of circuits in:

`Result2.txt`

## Reproducibility

The source codes are provided to document the computational procedure used
for identifying TF–miRNA–mRNA regulatory circuits.

## Citation

If you use this code, please cite the associated publication in
which the workflow is described.

## License

This repository is provided for research and academic use.
