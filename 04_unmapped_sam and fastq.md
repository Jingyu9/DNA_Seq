##The original SAM files **250G** in 3_bwa Directory of Newton, after filtering, **28G** unmapped SAM files were generated in 4_unmapped_sam Directory of Newton. Each of original SAM file is about **840M** and each of unmapped SAM file is about **95M** 

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

SamToFASTQ \
I=../4_unmapped_sam/SCNr3.unmapped.sam$SGE_TASK_ID \
FASTQ=SCNr3.unmapped.fastq$SGE_TASK_ID     
     


     

