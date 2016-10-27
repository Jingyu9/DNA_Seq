##Create a new directory 6_MapToViralGenomes
```
mkdir 6_MApToViralGenomes
cd 6_MapToViralGenomes
```
##Download the Viral Genomes from ftp://ftp.ncbi.nlm.nih.gov/refseq/release/viral/

```
wget ftp://ftp.ncbi.nlm.nih.gov/refseq/release/viral/viral.1.1.genomic.fna.gz
wget ftp://ftp.ncbi.nlm.nih.gov/refseq/release/viral/viral.2.1.genomic.fna.gz
gunzip viral.1.1.genomic.fna.gz
gunzip viral.2.1.genomic.fna.gz
cat viral.1.1.genomic.fna viral.1.1.genomic.fna > viral_102716.genomic.fna
```


```
#$ -N bwa
#$ -cwd
#$ -S /bin/bash
#$ -q medium*
#$ -l mem=6G,h_vmem=6G
#$ -t 1-305

module load bwa
bwa mem \
-t 1 \
../../rawdata/GCA_000150805.1_HG2_genomic.fna \
../2_trimmomatic/SCNr3_1.trimmed.paired.fastq$SGE_TASK_ID \
../2_trimmomatic/SCNr3_2.trimmed.paired.fastq$SGE_TASK_ID \
> SCNr3.sam$SGE_TASK_ID
```
