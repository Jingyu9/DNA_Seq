##Creat a new trimming directory under analysis directory 
```
mkdir 2_trimmomatic
cd 2_trimmomatic
```
##Write a script "trim.qsh"

```
nano trim.qsh
---------------------------------------------------
#$ -N Trim
#$ -cwd
#$ -S /bin/bash
#$ -q medium*
#$ -l mem=40G,h_vmem=40G
#$ -pe threads 2

module load trimmomatic
trimmomatic PE \
-phred33 \
../../rawdata/JLSCNr3_S99_L005_R1_001.fastq.gz \
../../rawdata/JLSCNr3_S99_L005_R2_001.fastq.gz \
SCNr3_1.trimmed.paired.fastq \
SCNr3_1.trimmed.unpaired.fastq \
SCNr3_2.trimmed.paired.fastq \
SCNr3_2.trimmed.unpaired.fastq \
SLIDINGWINDOW:4:10 MINLEN:36
----------------------------------------------------
```
##Submit the job to Newton
```
qsub trim.qsh
qstat # check the status
```
#Result
----------------------------------------------------------------------------------------------------------------------------------------
**After about 2h, total 202G files generated, including R1.trimmed.paired.fastq (102G), R2.trimmed.paired.fastq (101G),** 
**R1.unpaired.fastq (1.1M), R2.unpaired.fastq (32K),Trim.e(475),Trim.o(0),2 Trim.po(0)**

**Trim.e file showed "showing Input Read Pairs: 304730696 Both Surviving: 304727309 (100.00%) Forward Only Surviving: 3293 (0.00%) Reverse Only Surviving: 93 (0.00%) Dropped: 1 (0.00%) TrimmomaticPE: Completed successfully."**
--------------------------------------------------------------------------------------------------------------------------------------
##Create a directory "fastqc" and run fastqc to check the quality of the trimmed sequences.
```
mkdir fastqc
cd fastqc
qrsh -pe threads 2 -l mem=4G # Then go to the /2_trimmomatic/fastqc directory again
module load fastqc
fastqc -t 2 -o . ../SCNr3_1.trimmed.paired.fastq
fastqc -t 2 -o . ../SCNr3_2.trimmed.paired.fastq
fastqc -t 2 -o . ../SCNr3_1.trimmed.unpaired.fastq
fastqc -t 2 -o . ../SCNr3_2.trimmed.unpaired.fastq
```
![GitHub Logo](https://www.google.com/search?q=github+logo&espv=2&biw=1440&bih=794&tbm=isch&imgil=EjYxU3xL8GCuTM%253A%253BH8p6HHzcTglWAM%253Bhttps%25253A%25252F%25252Fgithub.com%25252Flogos&source=iu&pf=m&fir=EjYxU3xL8GCuTM%253A%252CH8p6HHzcTglWAM%252C_&usg=__MKO_rLjelXATqp1iwpCPkyKOPpY%3D&ved=0ahUKEwiXg4WigOLPAhUK4yYKHTD1DTAQyjcIPA&ei=ytkEWJf2OorGmwGw6reAAw#imgrc=EjYxU3xL8GCuTM%3A)
