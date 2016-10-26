##In 5_unmapped_fastq directory, run the following script.
```
#$ -N ExtractUnmappedFastq
#$ -cwd
#$ -S /bin/bash
#$ -q medium*
#$ -l mem=12G,h_vmem=12G
#$ -t 1-305

cat ../4_unmapped_sam/SCNr3.unmapped.sam$SGE_TASK_ID | grep -v ^@ | awk 'NR%2==1 {print "@"$1"\n"$10"\n+\n"$11}' > SCNr3.unmapped.1.fastq$SGE_TASK_ID
cat ../4_unmapped_sam/SCNr3.unmapped.sam$SGE_TASK_ID | grep -v ^@ | awk 'NR%2==0 {print "@"$1"\n"$10"\n+\n"$11}' > SCNr3.unmapped.2.fastq$SGE_TASK_ID
```
Total **26G** fastq file(R1 and R2) generated, each fastq file is 43M
