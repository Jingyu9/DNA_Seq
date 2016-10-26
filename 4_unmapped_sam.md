#The orignal SAM files 250G in 3_bwa Directory of Newton, after filtering, 28G unmapped SAM files were generated in 4_unmapped_sam Directory of Newton.

## Extract the R1 and R2 fastq files using Picard's SamToFastq

https://broadinstitute.github.io/picard/command-line-overview.html#SamToFastq


```
SamToFASTQ \
     I=input.bam \
     FASTQ=output.fastq
     
