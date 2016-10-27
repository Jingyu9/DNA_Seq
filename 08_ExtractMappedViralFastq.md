##Create a new directory
```
mkdir 8_ExtractMappedViralFastq
cd 8_ExtractMappedViralFastq
```
##Write a script(nano ExtractMappedFastq.qsh)

```
#$ -N ExtractMappedFastq
#$ -cwd
#$ -S /bin/bash
#$ -q medium*
#$ -l mem=6G,h_vmem=6G
#$ -t 1-305

cat ../7_FilterMappedViralSam/SCNr3.FilteredViralReads.sam$SGE_TASK_ID | grep -v ^@ | awk 'NR%2==1 {print "@"$1"\n"$10"\n+\n"$11}' > SCNr3.MappedViral.1.fastq$SGE_TASK_ID
cat ../7_FilterMappedViralSam/SCNr3.FilteredViralReads.sam$SGE_TASK_ID | grep -v ^@ | awk 'NR%2==0 {print "@"$1"\n"$10"\n+\n"$11}' > SCNr3.MappedViral.2.fastq$SGE_TASK_ID
```
##Result: Total generate **584M** R1 and R2 Mapped Viral Fastq files

##Combine all the R1 fastq (305) reads to a whole _SCNr3_MappedViral.R1.fastq_(**293M**)
```
cat SCNr3.MappedViral.1.fastq* > SCNr3_MappedViral.R1.fastq
```

##Combine all the R2 fastq (305) reads to a whole _SCNr3_MappedViral.R2.fastq_(**291M**)
```
cat SCNr3.MappedViral.2.fastq* > SCNr3_MappedViral.R2.fastq
```
##Count the number of reads in R1 (**88,8137 reads**) and R1 fastq files (**88,8077 reads**)
```
grep @K00 -c SCNr3_MappedViral.R1.fastq # 888137 reads
or
wc -l SCNr3_MappedViral.R1.fastq #3552548 SCNr3_MappedViral.R1.fastq, 3552548/4 = 888137 reads 

grep @K00 -c SCNr3_MappedViral.R2.fastq # 888077 reads
or
wc -l SCNr3_MappedViral.R2.fastq #3552308 SCNr3_MappedViral.R2.fastq, 3552308/4 = 888077 reads 
```
