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
#$ -l mem=12G,h_vmem=12G
#$ -t 1-305

cat ../4_unmapped_sam/SCNr3.unmapped.sam$SGE_TASK_ID | grep -v ^@ | awk 'NR%2==1 {print "@"$1"\n"$10"\n+\n"$11}' > SCNr3.unmapped.1.fastq$SGE_TASK_ID
cat ../4_unmapped_sam/SCNr3.unmapped.sam$SGE_TASK_ID | grep -v ^@ | awk 'NR%2==0 {print "@"$1"\n"$10"\n+\n"$11}' > SCNr3.unmapped.2.fastq$SGE_TASK_ID
```

##Combine all the R1 fastq (305) reads to a whole **SCNr3_MappedViral.R1.Fastq**
##Combine all the R2 fastq (305) reads to a whole **SCNr3_MappedViral.R2.Fastq**
