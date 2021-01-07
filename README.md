# PairwiseAlignment
Pairwise Alignment and comparison of Drosophila MEF2 and Human MEF2C

This script is written to compare and contrast the Drosophila MEF2 (dMEF2) protein with the human MEF2C (hMEF2C) protein to discover whether dMEF2 might be used as a homolog in the genetic studies of Neurodegenration diseases. This spipeline could equally be applied to align any two sequences however, has only been tested on these small MEF2 proteins.

**To run:**

  **1.** Download the python notebook in this repository.
 
  **2.** For sample data, download the fasta files in this repository. Make sure that the notebook & sample datafiles are located in a single directory. 
 
**Run the pipeline.**

**3.** If using different sequences, you will need to edit the filenames and change the sequences for local alignment in order to compare your sequences of interest. It is possible to use this pipeline with sequences in other formats such as using GenBank files however, please note that the code will need to be editted when uploading these files with SeqIO.parse. You can change the mismatch score (-10) and gap penalty (-0.5) and should you be comparing DNA or RNA sequences, one should consider which substitution matrix to apply as BLOSUM62 is specific for protein sequences.

In the analysis of dMEF2 and hMEF2C, we found that the MADS-Box and MEF2 domain at the N-terminus of the protein is extremely well conserved however, the hMEF2C Transcription Repressor and Ser/Thr Domains were not conserved and creates additional queries about whether dMEF2 may be used as a hMEF2C homolog.






