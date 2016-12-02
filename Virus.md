##Download virus genome

##Change format to txt

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
