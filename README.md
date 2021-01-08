# PairwiseAlignment
Pairwise Alignment and comparison of Drosophila MEF2 and Human MEF2C

## Table of Content

* [Introduction](##Introduction)
* [Technologies](##technologies)
* [Installation](##Installation)
* [Biopython](##Biopython-workflow-and-uploading-sequences-of-interest)
* [Pairwise Alignment](##Pairwise-Alignment-workflow)
* [Inspiration](##Inspiration)

## Introduction
This script was written to compare and contrast the Drosophila MEF2 (dMEF2) protein with the human MEF2C (hMEF2C) protein to discover whether dMEF2 might be used as a homolog in the genetic studies of Neurodegenerative diseases. This pipeline could equally be applied to align any two sequences of interest however, has only been tested on these relatively short sequences. 

## Technologies
The project was created with: 
* Anaconda Navigator (Anaconda3)
* JupyterLab 2.2.6
* Biopython 1.78

## Installation

  **1.** Download the python notebook in this repository.
 
  **2.** For sample data, download the fasta files in this repository. Make sure that the notebook & sample datafiles are located in a single directory. 

You will need to make sure that `Biopython` is installed on your device for analysis of DNA, RNA, and proteins.

```ruby
pip install biopython
```

Once Biopython is installed, you will be able to run the appropriate commands and use subpackages which are imported throughout the python Notebook.
 

## Biopython workflow and uploading sequences of interest

In order to understand the potential use of dMEF2 as a hMEF2C homolog in genetic studies of Neurodegenerative disease, we have built a coding pipeline which will enable transcription and translation of DNA to RNA and protein for subsequent global sequence alignment and local alignment of domains highly conserved within the human MEF2C protein.

**1.** With Biopython installed the pipeline started by importing the subpackages that are required for uploading the FASTA sequences and creating the Seq Object for DNA tracscription and RNA translation. These can be found in line 2 of the python Notebook.

**2.** Read in the dMEF2 FASTA sequence using `SeqIO.parse` and create a Seq object. If using different sequences, you will need to edit the filnames, It is possible to use this pipeline with sequences in other formats such as using GenBank files however, please note that the code will need to be editted when uploading these files with `SeqIO.parse`. 

```ruby
for dMEF2_dna in SeqIO.parse("dMEF2_dna.fasta", "fasta")
Seq = dMEF2_dna.seq
```

**3.** Transcribe the sequences into RNA and further create an RNA codon table for translation into protein.

```ruby
dMEF2_rna = ""
for i in Seq:
  if i == "T"
    dMEF2_rna += "U"
  else:
   dMEF2_rna += i
   
for i in range(0, len(dMEF2_rna)-(3+len(dMEF2_rna)%3), 3):
  codon = dMEF2_rna[i:i + 3]
  amino_acid = rna_codon.get(codon, "")
  prot_seq += amino_acid
print("Protein String: ", prot_seq
```

**4.** Upload the hMEF2C FASTA sequence for Pairwise sequence alignment. As before, if using different sequences, ensure that the filenames are editted and appropriate changes to code are made for different formats. 


## Pairwise Alignment Workflow

**5.** Import the appropriate subpackages for alignment and create a PairwiseAligner object (line 16 of Python Notebook).

**6.** Load `BLOSUM62` substitution matrix and calculate the global alignment of the sequences. You can change the mismatch score (-10) and gap penalty (-0.5) and should you be comparing DNA or RNA sequences, one should consider which substitution matrix to apply as BLOSUM62 is specific for protein sequences.

```ruby
from Bio.Align import substitution_matrices
matrix = substitution_matrices.load("BLOSUM62")
aligner.substitution_matrices = matrix

alignments = pairwise2.align.globalds(Seq1, Seq2, matrix, -10, -0.5)
```

**7.** Perform local alignment for specific domains or regions of interest. If using different sequences, you will need to change the sequences in order to compare your regions of interest. Sequences in this pipeline are taken from known understanding of the conserved domains within the hMEF2C protein. 

```ruby
alignements = aligner.align('Sequence1', 'Sequence2')
alignment = alignments[0]
print(alignment)
```

**7b.** For lengthier domains or regions of interest, we found it beneficial to run the local `pairwise2` function to enable formatting of the alignment.

```ruby
alignments = pairwise2.align.localds('Sequence1', 'Sequence2')
alignment = alignments[0]
print(pairwise2.format_alignment(*alignments[0])
```

## Inspiration 

This code was created with the help of the [Biopython Tutorial and Cookbook](http://biopython.org/DIST/docs/tutorial/Tutorial.html)

In the analysis of dMEF2 and hMEF2C, we found that the MADS-Box and MEF2 domain at the N-terminus of the protein is extremely well conserved however, the hMEF2C Transcription Repressor and Ser/Thr Domains were not conserved and creates additional queries about whether dMEF2 may be used as a hMEF2C homolog.






