##Download reference genome
Under **rawdata** directory, download reference genome from NCBI
Get the [reference genome][https://www.ncbi.nlm.nih.gov/genome/?term=soybean%20cyst%20nematode] , which will use to map the reads against.

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
##index the genome
```
module load bwa
bwa index ../../rawdata/GCA_000150805.1_HG2_genomic.fna
```
##Now we can do the alignment
```
bwa mem \
-t 2 \
~/e_coli/raw_data/GCF_000005845.2_ASM584v2_genomic.fna \
../2_trimmomatic/DRR021342_1.trimmed.paired.fastq \
../2_trimmomatic/DRR021342_2.trimmed.paired.fastq \
> DRR021342.sam
```
