##Download virus genome
###Download the Viral Genomes from ftp://ftp.ncbi.nlm.nih.gov/refseq/release/viral/ to rawdata directory and combine the viral.1.1.genomic.fna and viral.2.1.genomic.fna 

Download viral genomes
```
wget ftp://ftp.ncbi.nlm.nih.gov/refseq/release/viral/viral.1.1.genomic.fna.gz
wget ftp://ftp.ncbi.nlm.nih.gov/refseq/release/viral/viral.2.1.genomic.fna.gz

gunzip viral.1.1.genomic.fna.gz
gunzip viral.2.1.genomic.fna.gz
cat viral.1.1.genomic.fna viral.2.1.genomic.fna > viral_102716.genomic.fna--this file was created on 10/27/2016
```

Download viral protein sequences
```
wget ftp://ftp.ncbi.nlm.nih.gov/refseq/release/viral/viral.1.protein.faa.gz
wget ftp://ftp.ncbi.nlm.nih.gov/refseq/release/viral/viral.2.protein.faa.gz
gunzip viral.1.protein.faa.gz
gunzip viral.2.protein.faa.gz
cat viral.1.protein.faa viral.2.protein.faa > viral_120716.protein.faa--this file was created on 12/07/2016
```

##Change format to txt
Open by notepade, then save as txt

##Extract the annotation part and save it into viral_genome_annotation.txt
```
grep '>' viral_102716.txt > viral_genome_annotation.txt
```
##Load viral_genome_annotation to Excel and only leave the VirusID and Discription
see blow

VirusID	| Description
--------|------------
NC_021865.1	| Paenibacillus phage phiIBB_Pl23, complete genome
NC_020479.1	| Bacillus phage Curly, complete genome
NC_021857.1	| Shigella phage SfII, complete genome
... | ...

##Total number viral genome is 7445 (10/27/2016)
