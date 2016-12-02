##Download virus genome
###Download the Viral Genomes from ftp://ftp.ncbi.nlm.nih.gov/refseq/release/viral/ to rawdata directory and combine the viral.1.1.genomic.fna and viral.2.1.genomic.fna 
```
cat viral.1.1.genomic.fna viral.2.1.genomic.fna > viral_102716.genomic.fna--this file was created on 10/27/2016
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
