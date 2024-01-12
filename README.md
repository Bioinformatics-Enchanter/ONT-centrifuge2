# ONT-centrifuge2

This is analysis of oxford nanopore Sequencing platform long reads of bacterial DNA.

# Tools used

#seqKit

-   SeqKit -- a cross-platform and ultrafast toolkit for FASTA/Q file manipulation Version: 2.6.1 - Summary of Fastq file were generated using seqkit.

```{bash}
seqkit stat file.fastq # to check summary of fastq file 
seqkit seq -m 1000 -M 40000 basecalls.fastq > filtered.fastq #to filter read that were below 1000 and more than 40000
```
#guppy base caller 
- Guppy Basecalling Software, (C) Oxford Nanopore Technologies plc. Version 6.5.7+ca6d6af, minimap2 version 2.24-r1122. 
- Guppy was discontinued, thats why we didnot use it further.

#Dorado Basecaller 
- Dorado is Software developed by Oxford Nanopore. - Dorado version used for this analysis was 0.5.1+a7fb3e3.
- Base were called in pod5 files from MinIons using [sup\@v4.2.0] model and fastq file were generated.

```{bash}
# to basecall from pod5.file  
dorado basecaller sup@v4.2.0 path/to/file/pod5/ --emit-fastq -r > path/to/store/dorado_output/basecalls.fastq
```
#NanoPlot for Quality visualization - NanoPlot 1.42.0 is used for qc visualtation of fastq files generated from Dorado basecaller.

```{bash}
# to generate quality control visualization plot 
 NanoPlot --fastq path/to/data/filename.fastq
 
```
#Centrifuge taxonomic classifier 
- Centrifuge-class version 1.0.4 64-bit Built on Nebula Fri Jan 5 09:08:09 AM EST 2024 Compiler: gcc version 11.4.0 (Ubuntu 11.4.0-1ubuntu1\~22.04) version 1.0.4 metagenomics classifier 
- Reference database: Bacteria,Archaea (compressed) 6.3 GB Last updated: 4/15/2018
- Reads were classified using centrifuge

```{bash}
# to run centrifuge make sure database index is created or download from website
centrifuge -x pathway/to/databse/p_compressed \
-U path/to/input/fastq \
-S report.txt -report-file report.centrifuge.tsv

# to generate Kraken2 like report 
centrifuge-kreport -x pathway/to/databse/p_compressed path/tocentrifuge_output/report.txt > report.centrifuge.kreport.txt

```