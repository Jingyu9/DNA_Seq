##Create a new directory
```
mkdir 7_FilterMappedViralSam
cd 7_FilterMappedViralSam
```
##Filter Mapped Viral Sam files
https://broadinstitute.github.io/picard/explain-flags.html
Based on the above samtools flag information, SAM Flag: **-f 3** extract the following reads 
- [x]   read paired
- [x]   read mapped in proper pair

##Write a script (nano FilterMappedViralReads.qsh) 
```
#$ -N FilterMappedViralReads
#$ -cwd
#$ -S /bin/bash
#$ -q medium*
#$ -l mem=6G,h_vmem=6G
#$ -t 1-305

module load samtools

samtools view -f 3 ../6_MapToViralGenomes/SCNr3_MapToViral.sam$SGE_TASK_ID > SCNr3.FilteredViralReads.sam$SGE_TASK_ID
```
##Result: Total **771M** SAM files were generated,the size of each sam file varies **from 0 to 7.4M**.

#Troubleshooting on the fastq file extraction from SAM file
1. combine all the sam file into one SAM file
```
cat SCNr3.FilteredViralReads.sam* > SCNr3.FilteredViralReads.sam_total
```
Still **771M** SAM file
2. check the number of the reads
```
grep K00179 -c SCNr3.FilteredViralReads.sam_total
```
Get 1,776,214 reads containing both forward and reverse reads






