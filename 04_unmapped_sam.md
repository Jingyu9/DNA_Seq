##Filter all reads with a mapping to SCN, generating a new pair of read files that are all non-SCN reads

Create a new directory 4_unmapped_sam
```
mkdir 4_unmmapped_sam
cd 4_unmapped_sam
```
Write a FilterUnmapped.qsh file
```
#$ -N FilterUnmapped
#$ -cwd
#$ -S /bin/bash
#$ -q medium*
#$ -l mem=6G,h_vmem=6G
#$ -t 1-305

module load samtools

samtools view -f 12 ../3_bwa/SCNr3.sam$SGE_TASK_ID > SCNr3.unmapped.sam$SGE_TASK_ID
```
##The original SAM files **250G** in 3_bwa Directory of Newton, after filtering, **28G** unmapped SAM files were generated in 4_unmapped_sam Directory of Newton. Each of original SAM file is about **840M** and each of unmapped SAM file is about **95M** 

```
cd ..
mkdir 5_unmapped_fastq
cd 5_unmapped_fastq
```

## Extract the R1 and R2 fastq files using Picard's SamToFastq (In Newton, picard/2.6.0 is available)
https://broadinstitute.github.io/picard/command-line-overview.html#SamToFastq


```
#$ -N ExtractUnmappedFastq
#$ -cwd
#$ -S /bin/bash
#$ -q medium*
#$ -l mem=6G,h_vmem=6G
#$ -t 1-305

module load picard

picard SamToFastq \
I=../4_unmapped_sam/SCNr3.unmapped.sam$SGE_TASK_ID \
FASTQ=SCNr3.unmapped.1.fastq$SGE_TASK_ID \
SECOND_END_FASTQ=SCNr3.unmapped.2.fastq$SGE_TASK_ID


picard SamToFastq \
INPUT=../4_unmapped_sam/SCNr3.unmapped.sam1 \
FASTQ=SCNr3.unmapped.fastq.1. \
SECOND_END_FASTQ=SCNr3.unmapped.2.fastq1
```
The above picard command works individually, but not in the script.
## Extract R1 and R2 fastq file from the SAM file using the following template which contains cat and awk command 
```
cat samplename.nomapping.sam | grep -v ^@ | awk 'NR%2==1 {print "@"$1"\n"$10"\n+\n"$11}' > unmapped/samplename_1.fastq 
cat samplename.nomapping.sam | grep -v ^@ | awk 'NR%2==0 {print "@"$1"\n"$10"\n+\n"$11}' > unmapped/samplename_2.fastq
```

The following is my script (nano ExtractUnmappedFastq_linux.qsh)
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

```
cat ../4_unmapped_sam/SCNr3.unmapped.sam$SGE_TASK_ID | grep -v ^@ | awk '$2==77 {print "@"$1"\n"$10"\n+\n"$11}' > SCNr3.unmapped.1.fastq$SGE_TASK_ID
cat ../4_unmapped_sam/SCNr3.unmapped.sam$SGE_TASK_ID | grep -v ^@ | awk '$2==141 {print "@"$1"\n"$10"\n+\n"$11}' > SCNr3.unmapped.2.fastq$SGE_TASK_ID
```

```


     

