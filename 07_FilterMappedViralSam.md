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


