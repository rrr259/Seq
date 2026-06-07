# Seq

Seq is a Python 3 command-line workflow for protein sequence analysis. The script searches NCBI taxonomy and protein databases, downloads protein sequences in FASTA format, performs sequence alignment, scans protein motifs, predicts secondary structure, calculates protein statistics, and generates summary plots.

## Repository contents

- `Script` - main Python script for the analysis workflow.
- `Seq_report.pdf` - project report/documentation.

## What the script does

The workflow:

1. Creates a working directory called `ICA2_programme`.
2. Asks the user for a taxonomy name.
3. Searches NCBI Taxonomy and lets the user choose the correct taxonomic group.
4. Retrieves the taxonomy ID.
5. Asks for a protein name.
6. Searches NCBI Protein for matching non-predicted and non-hypothetical sequences.
7. Downloads up to 1000 protein sequences as `protein_sequences.fasta`.
8. Aligns the sequences with Clustal Omega.
9. Creates conservation plots using EMBOSS `plotcon`.
10. Searches PROSITE motifs using EMBOSS `patmatmotifs`.
11. Exports motif counts to `motif_data.csv`.
12. Creates a stacked motif bar plot as `bar_plot.png`.
13. Predicts protein secondary structure using EMBOSS `garnier`.
14. Calculates protein properties using EMBOSS `pepstats`.
15. Exports protein statistics to `pepstats_data.csv`.

## Requirements

Python packages:

- `pandas`
- `matplotlib`

External command-line tools:

- NCBI EDirect tools: `esearch`, `efetch`
- Clustal Omega: `clustalo`
- EMBOSS tools:
  - `plotcon`
  - `patmatmotifs`
  - `garnier`
  - `pepstats`

The script also calls `eog` to open an image file, which is commonly available on Linux desktop systems.

## Installation

Clone the repository:

```bash
git clone https://github.com/rrr259/Seq.git
cd Seq
```

Install Python dependencies:

```bash
pip install pandas matplotlib
```

Install the required bioinformatics command-line tools separately. For example, on Ubuntu/Debian systems:

```bash
sudo apt install clustalo emboss
```

NCBI EDirect installation instructions are available from NCBI:
https://www.ncbi.nlm.nih.gov/books/NBK179288/

## Usage

Run the script with Python 3:

```bash
python3 Script
```

The program is interactive. It will ask for:

- a taxonomy name, for example `Mammalia`, `Aves`, or another taxonomic group
- a protein name, for example `cytochrome c`
- whether to continue with the dataset found
- whether to include simple post-translational modification sites during motif analysis

## Output files

The script creates a new directory called `ICA2_programme` and stores the analysis results there.

Main output files include:

- `protein_sequences.fasta` - downloaded protein sequences
- `aligment.msf` - multiple sequence alignment output
- `platcon.1.pdf` - sequence conservation plot
- `platcon.1.png` - sequence conservation plot image
- `Patmatmotifs_files/` - motif scan results for each sequence
- `patmotifs_all` - combined motif results
- `motif_data.csv` - motif count table
- `bar_plot.png` - stacked bar plot of motif counts
- `report.garnier` - predicted protein secondary structure
- `Pepstats_files/` - protein statistics for each sequence
- `pepstats_all` - combined pepstats output
- `pepstats_data.csv` - parsed protein statistics table

## Notes

- The script deletes and recreates the `ICA2_programme` directory each time it runs.
- Datasets with 0 sequences or more than 1000 sequences are rejected.
- Protein and taxonomy names must be spelled carefully because the NCBI search depends on the input text.
- Some external tools may need to be added to your system `PATH` before running the script.

## Author

Created by `rrr259`.
