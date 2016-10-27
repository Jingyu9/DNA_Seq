##Download the Viral Genomes from ftp://ftp.ncbi.nlm.nih.gov/refseq/release/viral/ to rawdata directory and combine the viral.1.1.genomic.fan and viral.2.1.genomic.fan

Index of /refseq/release/viral/
Name	Size	Date Modified
[parent directory]		
viral.1.1.genomic.fna.gz	58.0 MB	9/9/16, 5:43:00 PM
viral.1.genomic.gbff.gz	153 MB	9/9/16, 5:44:00 PM
viral.1.protein.faa.gz	37.2 MB	9/9/16, 5:43:00 PM
viral.1.protein.gpff.gz	82.0 MB	9/9/16, 5:43:00 PM
viral.2.1.genomic.fna.gz	6.9 MB	9/9/16, 5:43:00 PM
viral.2.genomic.gbff.gz	18.2 MB	9/9/16, 5:43:00 PM
viral.2.protein.faa.gz	4.5 MB	9/9/16, 5:43:00 PM
viral.2.protein.gpff.gz	9.7 MB	9/9/16, 5:43:00 PM
viral.nonredundant_protein.1.protein.faa.gz	13.8 kB	9/9/16, 5:43:00 PM
viral.nonredundant_protein.1.protein.gpff.gz	34.4 kB	9/9/16, 5:43:00 PM

```
wget ftp://ftp.ncbi.nlm.nih.gov/refseq/release/viral/viral.1.1.genomic.fna.gz
wget ftp://ftp.ncbi.nlm.nih.gov/refseq/release/viral/viral.2.1.genomic.fna.gz
gunzip viral.1.1.genomic.fna.gz
gunzip viral.2.1.genomic.fna.gz
cat viral.1.1.genomic.fna viral.1.1.genomic.fna > viral_102716.genomic.fna
```
##Create a new directory 6_MapToViralGenomes
```
mkdir 6_MApToViralGenomes
cd 6_MapToViralGenomes
```
##Create index of viral genomes
```
module load bwa
bwa index ../../rawdata/viral_102716.genomic.fna
```

##Write a script (nano MapToViral.qsh)
```
#$ -N MapToViral_bwa
#$ -cwd
#$ -S /bin/bash
#$ -q medium*
#$ -l mem=6G,h_vmem=6G
#$ -t 1-305

module load bwa
bwa mem \
-t 1 \
../../rawdata/viral_102716.genomic.fna \
../5_unmapped_fastq/SCNr3.unmapped.1.fastq$SGE_TASK_ID \
../5_unmapped_fastq/SCNr3.unmapped.2.fastq$SGE_TASK_ID \
> SCNr3_MapToViral.sam$SGE_TASK_ID
```
##Result:
**28G _SCNr3_MapToViral.sam_** were generated, each sam file is about 94M.
