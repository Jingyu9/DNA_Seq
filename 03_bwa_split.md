##Go the 2_trimmomatic directory and use interactive mode (qrsh)

###split the files
```
split -l 4000000 -d -a 3 SCNr3_1.trimmed.paired.fastq SCNr3_1.trimmed.paired.fastq
split -l 4000000 -d -a 3 SCNr3_2.trimmed.paired.fastq SCNr3_2.trimmed.paired.fastq
```
**There are 305 child-fastq files (fastq000 to fastq304) generated.**
###Change file000 to file305
```
mv SCNr3_1.trimmed.paired.fastq000 SCNr3_1.trimmed.paired.fastq305
```

###rename the files (deleting the leading zero for next step)
rename from to file...
Description
rename will rename the specified files by replacing the first occurrence of from in their name by to.
For example, given the files
foo1, ..., foo9, foo10, ..., foo278, the commands
rename foo foo0 foo?
rename foo foo0 foo??
will turn them into foo001, ..., foo009, foo010, ..., foo278.
And
rename .htm .html *.htm
will fix the extension of your html files.
```
rename SCNr3_1.trimmed.paired.fastq0 SCNr3_1.trimmed.paired.fastq SCNr3_1.trimmed.paired.fastq0*
rename SCNr3_1.trimmed.paired.fastq0 SCNr3_1.trimmed.paired.fastq SCNr3_1.trimmed.paired.fastq0*

rename SCNr3_2.trimmed.paired.fastq0 SCNr3_2.trimmed.paired.fastq SCNr3_2.trimmed.paired.fastq0*
rename SCNr3_2.trimmed.paired.fastq0 SCNr3_2.trimmed.paired.fastq SCNr3_2.trimmed.paired.fastq0*
```

##Write a bwa_split.qsh file, the index numbers will be exported to the job tasks via the **environment variable $SGE_TASK_ID**
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
Result: SCNr3.sam1 to SCNr3.sam305 were generated.

##Filter all reads with a mapping to SCN, generating a new pair of read files that are all non-SCN reads
###Create a new directory 4_unmapped_sam
```
cd ..
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

