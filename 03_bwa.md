##Download reference genome
Under **rawdata** directory, download reference genome from NCBI
Get the [reference genome](https://www.ncbi.nlm.nih.gov/genome/?term=soybean%20cyst%20nematode) , which will use to map the reads against.

(ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA_000150805.1_HG2/GCA_000150805.1_HG2_genomic.fna.gz) ##24.4MB
```
cd rawdata
wget ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA_000150805.1_HG2/GCA_000150805.1_HG2_genomic.fna.gz
gunzip GCA_000150805.1_HG2_genomic.fna.gz
```
##Create a new directory 3_bwa under analysis directory
```
mkdir 3_bwa
cd 3_bwa
```
##Index the genome
```
module load bwa
bwa index ../../rawdata/GCA_000150805.1_HG2_genomic.fna
```
##Use the interactive mode and go to the correct directory
```
qrsh -pe threads 2 -l mem=4G
#cd 3_bwa 
```
##Do the alignment
```
bwa mem \
-t 2 \
../../rawdata/GCA_000150805.1_HG2_genomic.fna \
../2_trimmomatic/SCNr3_1.trimmed.paired.fastq \
../2_trimmomatic/SCNr3_2.trimmed.paired.fastq \
> SCNr3.sam
```
Or write a script and send a job to Newton
```
nano bwa.qsh
---------------------------------------------------
#$ -N bwa
#$ -cwd
#$ -S /bin/bash
#$ -q medium*
#$ -l mem=40G,h_vmem=40G
#$ -pe threads 2

module load bwa
bwa mem \
-t 2 \
../../rawdata/GCA_000150805.1_HG2_genomic.fna \
../2_trimmomatic/SCNr3_1.trimmed.paired.fastq \
../2_trimmomatic/SCNr3_2.trimmed.paired.fastq \
> SCNr3.sam
qsub bwa.qsh
```
_**HOW TO CHECK THE INTEGRITY OF SAM FILE SINCE IT TOOK MORE THAN 24h TO FINISH WITHOUT ANY NOTIFICATION?**_
```
nano flagtest.qsh
---------------------------------------------------
#$ -N flagtest
#$ -cwd
#$ -S /bin/bash
#$ -q medium*
#$ -l mem=10G,h_vmem=10G
#$ -pe threads 2

awk '{print $2}' SCNr3.sam | egrep '^[0-9]' | sort -n | uniq > flagtest_lin.txt
```
##Samtools (Visualizing the alignments)
```
module load samtools
```
###Convert to sorted bam, then index the bam file.
```
samtools sort -@ 2 -o SCNr3.bam SCNr3.sam
samtools index SCNr3.bam  
```
The -@ flag specifies the number of threads and the -o flag is used to specify the name of the output file.

To view, we need to index the reference as well. We'll create a symbolic link to the reference genome, for convenience. Its basically a file holder (not a real file) that **_points to_** the real file. You can see where it points with ls -l
```
ln -s ../../rawdata/GCA_000150805.1_HG2_genomic.fna
ls -l
```
###Now to index
```
samtools faidx GCA_000150805.1_HG2_genomic.fna
```
###Now we can try out the samtools viewer to see the mappings
```
samtools tview SCNr3.bam GCA_000150805.1_HG2_genomic.fna
```
