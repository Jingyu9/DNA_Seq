##Create a new directory
```
mkdir 9_assembly
cd 9_assembly
```
##Write a script (nano assemble.qsh)
```
#$ -N abyss
#$ -cwd
#$ -S /bin/bash
#$ -q medium*
#$ -l mem=10G,h_vmem=10G
#$ -pe threads 2

module load abyss
abyss-pe k=48 np=2 name=SCNr3_CandidateVirusContig \
in='../8_ExtractMappedViralFastq/SCNr3_MappedViral.R1.fastq ../8_ExtractMappedViralFastq/SCNr3_MappedViral.R2.fastq'
```
##Result:
```
####
[Newton:sigma00 9_assembly]$ ls -lh
total 22M
-rw-r--r-- 1 jlin11 users 1.2K Oct 27 17:23 abyss.e8754576
-rw-r--r-- 1 jlin11 users 5.9K Oct 27 17:21 abyss.o8754576
-rw-r--r-- 1 jlin11 users    0 Oct 27 16:57 abyss.pe8754576
-rw-r--r-- 1 jlin11 users    0 Oct 27 16:57 abyss.po8754576
-rw-r--r-- 1 jlin11 users  281 Oct 27 16:56 assemble.qsh
-rw-r--r-- 1 jlin11 users  30K Oct 27 17:00 coverage.hist
-rw-r--r-- 1 jlin11 users 2.9M Oct 27 17:21 SCNr3_CandidateVirusContig-1.dot
-rw-r--r-- 1 jlin11 users 4.7M Oct 27 17:21 SCNr3_CandidateVirusContig-1.fa
-rw-r--r-- 1 jlin11 users    0 Oct 27 17:21 SCNr3_CandidateVirusContig-1.path
-rw-r--r-- 1 jlin11 users 2.2M Oct 27 17:21 SCNr3_CandidateVirusContig-2.dot
-rw-r--r-- 1 jlin11 users 2.2M Oct 27 17:21 SCNr3_CandidateVirusContig-2.dot1
-rw-r--r-- 1 jlin11 users 4.0M Oct 27 17:21 SCNr3_CandidateVirusContig-2.fa
-rw-r--r-- 1 jlin11 users  19K Oct 27 17:21 SCNr3_CandidateVirusContig-2.path
-rw-r--r-- 1 jlin11 users 2.0M Oct 27 17:21 SCNr3_CandidateVirusContig-3.dot
-rw-r--r-- 1 jlin11 users 3.9M Oct 27 17:21 SCNr3_CandidateVirusContig-3.fa
-rw-r--r-- 1 jlin11 users   35 Oct 27 17:23 SCNr3_CandidateVirusContig-3.hist
-rw-r--r-- 1 jlin11 users 325K Oct 27 17:21 SCNr3_CandidateVirusContig-bubbles.fa
-rw-r--r-- 1 jlin11 users  72K Oct 27 17:21 SCNr3_CandidateVirusContig-indel.fa
lrwxrwxrwx 1 jlin11 users   31 Oct 27 17:21 SCNr3_CandidateVirusContig-unitigs.fa -> SCNr3_CandidateVirusContig-3.fa


 cat abyss.e8754576
`../8_ExtractMappedViralFastq/SCNr3_MappedViral.R1.fastq': discarded 39 reads shorter than 48 bases
`../8_ExtractMappedViralFastq/SCNr3_MappedViral.R1.fastq': discarded 1 reads containing non-ACGT characters
`../8_ExtractMappedViralFastq/SCNr3_MappedViral.R2.fastq': discarded 28 reads shorter than 48 bases
`../8_ExtractMappedViralFastq/SCNr3_MappedViral.R2.fastq': discarded 1 reads containing non-ACGT characters
The minimum coverage of single-end contigs is 1.88439.
The minimum coverage of merged contigs is 2.83333.
Consider increasing the coverage threshold parameter, c, to 2.83333.
Building the suffix array...
Building the Burrows-Wheeler transform...
Building the character occurrence table...
Mateless      112  0.0126%
Unaligned  335604  37.8%
Singleton   72960  8.21%
FR              6  0.000676%
RF              1  0.000113%
FF         295670  33.3%
Different  183810  20.7%
Total      888163
abyss-fixmate: error: The mate pairs of this library are oriented forward-forward (FF), which is not supported by ABySS.
make: *** [SCNr3_CandidateVirusContig-3.dist] Error 1
make: *** Deleting file `SCNr3_CandidateVirusContig-3.dist'

cat abyss.o8754576
/data/apps/openmpi/1.6.5-intel/bin/mpirun -np 2 ABYSS-P -k48 -q3    --coverage-hist=coverage.hist -s SCNr3_CandidateVirusContig-bubbles.fa  -o SCNr3_CandidateVirusContig-1.fa ../8_ExtractMappedViralFastq/SCNr3_MappedViral.R1.fastq ../8_ExtractMappedViralFastq/SCNr3_MappedViral.R2.fastq
ABySS 1.9.0
ABYSS-P -k48 -q3 --coverage-hist=coverage.hist -s SCNr3_CandidateVirusContig-bubbles.fa -o SCNr3_CandidateVirusContig-1.fa ../8_ExtractMappedViralFastq/SCNr3_MappedViral.R1.fastq ../8_ExtractMappedViralFastq/SCNr3_MappedViral.R2.fastq
Running on 2 processors
0: Running on host sigma39.local
1: Running on host sigma39.local
0: Reading `../8_ExtractMappedViralFastq/SCNr3_MappedViral.R1.fastq'...
1: Reading `../8_ExtractMappedViralFastq/SCNr3_MappedViral.R2.fastq'...
1: Loaded 13488613 k-mer.
0: Loaded 13709251 k-mer.
Loaded 27197864 k-mer. At least 870 MB of RAM is required.
Minimum k-mer coverage is 84
Using a coverage threshold of 3...
The median k-mer coverage is 8
The reconstruction is 8326254
The k-mer coverage threshold is 2.82843
Setting parameter e (erode) to 3
Setting parameter E (erodeStrand) to 1
Setting parameter c (coverage) to 2.82843
Finding adjacenct k-mer...
1: Added 27084163 edges.
0: Added 27519532 edges.
Added 54603695 edges.
Eroding tips...
1: Eroded 1117744 tips.
0: Eroded 11018840 tips.
0: Eroded 6523 tips.
Eroded 21832171 tips.
1: Eroded 9689064 tips.
Pruning tips shorter than 1 bp...
0: Pruned 186 tips.
1: Pruned 180 tips.
Pruned 366 k-mer in 366 tips.
Pruning tips shorter than 2 bp...
0: Pruned 144 tips.
1: Pruned 125 tips.
Pruned 457 k-mer in 269 tips.
Pruning tips shorter than 4 bp...
0: Pruned 217 tips.
1: Pruned 184 tips.
Pruned 1051 k-mer in 401 tips.
Pruning tips shorter than 8 bp...
0: Pruned 326 tips.
1: Pruned 296 tips.
Pruned 2761 k-mer in 622 tips.
Pruning tips shorter than 16 bp...
0: Pruned 437 tips.
1: Pruned 436 tips.
Pruned 7108 k-mer in 873 tips.
Pruning tips shorter than 32 bp...
0: Pruned 698 tips.
1: Pruned 714 tips.
Pruned 21179 k-mer in 1412 tips.
Pruning tips shorter than 48 bp...
0: Pruned 569 tips.
1: Pruned 607 tips.
Pruned 27313 k-mer in 1176 tips.
Pruning tips shorter than 48 bp...
0: Pruned 5 tips.
1: Pruned 3 tips.
Pruned 61 k-mer in 8 tips.
Pruning tips shorter than 48 bp...
0: Pruned 0 tips.
1: Pruned 0 tips.
Pruned 5127 tips in 8 rounds.
Marking ambiguous branches...
0: Marked 159306 edges of 72160 ambiguous vertices.
1: Marked 160837 edges of 72698 ambiguous vertices.
Marked 144858 ambiguous branches.
Removing low-coverage contigs (mean k-mer coverage < 2.82843)...
0: Found 2642162 k-mer in 95789 contigs before removing low-coverage contigs.
Removed 1173449 k-mer in 34340 low-coverage contigs.
1: Found 2658309 k-mer in 95036 contigs before removing low-coverage contigs.
Removed 1183786 k-mer in 33805 low-coverage contigs.
Found 5300471 k-mer in 190825 contigs before removing low-coverage contigs.
Removed 2357235 k-mer in 68145 low-coverage contigs.
Splitting ambiguous branches...
1: Split 67383 ambigiuous branches.
0: Split 68282 ambigiuous branches.
Split 135665 ambiguous branches.
Removed 2357235 marked k-mer.
Eroding tips...
1: Eroded 43713 tips.
0: Eroded 42620 tips.
1: Eroded 2564 tips.
0: Eroded 2260 tips.
Eroded 91157 tips.
Pruning tips shorter than 1 bp...
1: Pruned 265 tips.
0: Pruned 334 tips.
Pruned 599 k-mer in 599 tips.
Pruning tips shorter than 2 bp...
1: Pruned 180 tips.
0: Pruned 190 tips.
Pruned 615 k-mer in 370 tips.
Pruning tips shorter than 4 bp...
1: Pruned 201 tips.
0: Pruned 223 tips.
Pruned 1115 k-mer in 424 tips.
Pruning tips shorter than 8 bp...
0: Pruned 256 tips.
1: Pruned 207 tips.
Pruned 2179 k-mer in 463 tips.
Pruning tips shorter than 16 bp...
0: Pruned 270 tips.
1: Pruned 295 tips.
Pruned 4707 k-mer in 565 tips.
Pruning tips shorter than 32 bp...
0: Pruned 350 tips.
1: Pruned 361 tips.
Pruned 11614 k-mer in 711 tips.
Pruning tips shorter than 48 bp...
0: Pruned 185 tips.
1: Pruned 185 tips.
Pruned 9581 k-mer in 370 tips.
Pruning tips shorter than 48 bp...
0: Pruned 0 tips.
1: Pruned 0 tips.
Pruned 3502 tips in 7 rounds.
Popping bubbles...
0: Removed 1037 bubbles.
1: Removed 361 bubbles.
Removed 1398 bubbles.
Removed 1398 bubbles.
Marking ambiguous branches...
0: Marked 21328 edges of 9486 ambiguous vertices.
1: Marked 21898 edges of 9745 ambiguous vertices.
Marked 19231 ambiguous branches.
Assembling...
0: Assembled 1382954 k-mer in 17334 contigs.
1: Assembled 1358052 k-mer in 17042 contigs.
Assembled 2741006 k-mer in 34376 contigs.
Concatenating fasta files to SCNr3_CandidateVirusContig-1.fa
Concatenating fasta files to SCNr3_CandidateVirusContig-bubbles.fa
Done.
AdjList    -k48 -m50 --dot SCNr3_CandidateVirusContig-1.fa >SCNr3_CandidateVirusContig-1.dot
abyss-filtergraph  --dot   -k48 -g SCNr3_CandidateVirusContig-2.dot1 SCNr3_CandidateVirusContig-1.dot SCNr3_CandidateVirusContig-1.fa >SCNr3_CandidateVirusContig-1.path
MergeContigs   -k48 -g SCNr3_CandidateVirusContig-2.dot -o SCNr3_CandidateVirusContig-2.fa SCNr3_CandidateVirusContig-1.fa SCNr3_CandidateVirusContig-2.dot1 SCNr3_CandidateVirusContig-1.path
PopBubbles  --dot -j2 -k48  -p0.9  -g SCNr3_CandidateVirusContig-3.dot SCNr3_CandidateVirusContig-2.fa SCNr3_CandidateVirusContig-2.dot >SCNr3_CandidateVirusContig-2.path
MergeContigs   -k48 -o SCNr3_CandidateVirusContig-3.fa SCNr3_CandidateVirusContig-2.fa SCNr3_CandidateVirusContig-2.dot SCNr3_CandidateVirusContig-2.path
awk '!/^>/ {x[">" $1]=1; next} {getline s} $1 in x {print $0 "\n" s}' \
                SCNr3_CandidateVirusContig-2.path SCNr3_CandidateVirusContig-1.fa >SCNr3_CandidateVirusContig-indel.fa
ln -sf SCNr3_CandidateVirusContig-3.fa SCNr3_CandidateVirusContig-unitigs.fa
abyss-map   -j2 -l48    ../8_ExtractMappedViralFastq/SCNr3_MappedViral.R1.fastq ../8_ExtractMappedViralFastq/SCNr3_MappedViral.R2.fastq SCNr3_CandidateVirusContig-3.fa \
                |abyss-fixmate   -l48  -h SCNr3_CandidateVirusContig-3.hist \
                |sort -snk3 -k4 \
                |DistanceEst   -j2 -k48 -l48 -s200 -n10   -o SCNr3_CandidateVirusContig-3.dist SCNr3_CandidateVirusContig-3.hist
                
###
```
##Move all the above assemble result to a new created directory (k_48)

##Try a new assembly job with **K=34**, ---> Still not working

##Need to fix the error "abyss-fixmate: error: The mate pairs of this library are oriented forward-forward (FF), which is not supported by ABySS." Maybe check the R2 sequence and reverse compliment of it.
```
https://www.biostars.org/p/155094/
Well...  it looks like read 2 did not get reverse-complemented.  You can reverse-complement it with Reformat from the BBMap package:

reformat.sh in=read2.fq out=reversed.fq rcomp
Or if the reads are interleaved in a single file:

reformat.sh in=reads.fq out=reversed.fq rcompmate
```
[Newton:sigma00 k_48]$ abyss-fac SCNr3_CandidateVirusContig-1.fa
n       n:500   L50     min     N80     N50     N20     E-size  max     sum     name
34376   426     173     500     540     632     831     713     2226    280720  SCNr3_CandidateVirusContig-1.fa
[Newton:sigma00 k_48]$ abyss-fac SCNr3_CandidateVirusContig-2.fa
n       n:500   L50     min     N80     N50     N20     E-size  max     sum     name
23802   426     173     500     540     632     831     713     2226    280720  SCNr3_CandidateVirusContig-2.fa
[Newton:sigma00 k_48]$ abyss-fac SCNr3_CandidateVirusContig-3.fa
SCNr3_CandidateVirusContig-3.fa:0: warning: file is empty
n       n:500   L50     min     N80     N50     N20     E-size  max     sum     name
0       0       0       0       0       0       0       0       0       0       SCNr3_CandidateVirusContig-3.fa

you can resume an ABySS assembly where it left off, but there's no need to edit the abyss-pe script. By default, it will resume an aborted assembly where it left off (due to it's being a Makefile script). You can use the --dry-run option of abyss-pe (it's actually an option of make) to see which commands will be run.


## Combine all the sam file into ONE SAM file (), then run abyss

Still in short time it stop, only get SCNr3_CandidateVirusContig-1.fa, SCNr3_CandidateVirusContig-2.fa SCNr3_CandidateVirusContig-3.fa
The result is similar, The max is 2260 long sequence. No Statisc file was generated. so still has problem.

##Run abyss using the new R1 and R2 files generated from BAM file through picard command(8.3directory)
```
#$ -N abyss
#$ -cwd
#$ -S /bin/bash
#$ -q medium*
#$ -l mem=10G,h_vmem=10G
#$ -pe threads 2

module load abyss
abyss-pe k=34 np=2 name=SCNr3_CandidateVirusContig \
in='../8.3_ExtractMappedViralFastq/SCNr3.SortedViralFinalRead.R1.fastq ../8.3_ExtractMappedViralFastq/SCNr3.SortedViralFinalRead.R2.fastq
```
Get the following result
```
total 78M
-rw-r--r-- 1 jlin11 users 1.7K Nov  7 16:11 abyss.e8798607
-rw-r--r-- 1 jlin11 users 9.9K Nov  7 16:11 abyss.o8798607
-rw-r--r-- 1 jlin11 users    0 Nov  7 15:53 abyss.pe8798607
-rw-r--r-- 1 jlin11 users    0 Nov  7 15:53 abyss.po8798607
-rw-r--r-- 1 jlin11 users  225 Nov  7 15:00 assemble_bam.qsh
-rw-r--r-- 1 jlin11 users  303 Nov  7 15:53 assemble.qsh
-rw-r--r-- 1 jlin11 users  230 Nov  3 15:57 assemble_sam.qsh
-rw-r--r-- 1 jlin11 users    0 Nov  7 16:34 -c
-rw-r--r-- 1 jlin11 users  33K Nov  7 15:59 coverage.hist
drwxr-xr-x 2 jlin11 users 4.0K Nov  3 14:03 k_34
drwxr-xr-x 2 jlin11 users 4.0K Nov  7 14:58 k_34_sam
drwxr-xr-x 2 jlin11 users 4.0K Oct 28 11:22 k_48
-rw-r--r-- 1 jlin11 users 5.0M Nov  7 16:08 SCNr3_CandidateVirusContig-1.dot
-rw-r--r-- 1 jlin11 users 8.6M Nov  7 16:07 SCNr3_CandidateVirusContig-1.fa
-rw-r--r-- 1 jlin11 users    0 Nov  7 16:08 SCNr3_CandidateVirusContig-1.path
-rw-r--r-- 1 jlin11 users 4.2M Nov  7 16:08 SCNr3_CandidateVirusContig-2.dot
-rw-r--r-- 1 jlin11 users 4.2M Nov  7 16:08 SCNr3_CandidateVirusContig-2.dot1
-rw-r--r-- 1 jlin11 users 8.0M Nov  7 16:08 SCNr3_CandidateVirusContig-2.fa
-rw-r--r-- 1 jlin11 users  43K Nov  7 16:08 SCNr3_CandidateVirusContig-2.path
-rw-r--r-- 1 jlin11 users  19K Nov  7 16:10 SCNr3_CandidateVirusContig-3.dist
-rw-r--r-- 1 jlin11 users 3.8M Nov  7 16:08 SCNr3_CandidateVirusContig-3.dot
-rw-r--r-- 1 jlin11 users 7.7M Nov  7 16:08 SCNr3_CandidateVirusContig-3.fa
-rw-r--r-- 1 jlin11 users 1.2M Nov  7 16:10 SCNr3_CandidateVirusContig-3.fa.fai
-rw-r--r-- 1 jlin11 users 4.6K Nov  7 16:09 SCNr3_CandidateVirusContig-3.hist
-rw-r--r-- 1 jlin11 users 3.8M Nov  7 16:10 SCNr3_CandidateVirusContig-4.dot
-rw-r--r-- 1 jlin11 users   96 Nov  7 16:10 SCNr3_CandidateVirusContig-4.fa
-rw-r--r-- 1 jlin11 users   18 Nov  7 16:10 SCNr3_CandidateVirusContig-4.fa.fai
-rw-r--r-- 1 jlin11 users 6.4K Nov  7 16:10 SCNr3_CandidateVirusContig-4.path1
-rw-r--r-- 1 jlin11 users 5.6K Nov  7 16:10 SCNr3_CandidateVirusContig-4.path2
-rw-r--r-- 1 jlin11 users 5.6K Nov  7 16:10 SCNr3_CandidateVirusContig-4.path3
-rw-r--r-- 1 jlin11 users 3.8M Nov  7 16:10 SCNr3_CandidateVirusContig-5.dot
-rw-r--r-- 1 jlin11 users  865 Nov  7 16:10 SCNr3_CandidateVirusContig-5.fa
-rw-r--r-- 1 jlin11 users 5.8K Nov  7 16:10 SCNr3_CandidateVirusContig-5.path
-rw-r--r-- 1 jlin11 users 5.7K Nov  7 16:11 SCNr3_CandidateVirusContig-6.dist.dot
-rw-r--r-- 1 jlin11 users 3.8M Nov  7 16:10 SCNr3_CandidateVirusContig-6.dot
-rw-r--r-- 1 jlin11 users 7.7M Nov  7 16:10 SCNr3_CandidateVirusContig-6.fa
-rw-r--r-- 1 jlin11 users 4.7K Nov  7 16:11 SCNr3_CandidateVirusContig-6.hist
-rw-r--r-- 1 jlin11 users  157 Nov  7 16:11 SCNr3_CandidateVirusContig-6.path
-rw-r--r-- 1 jlin11 users  19K Nov  7 16:11 SCNr3_CandidateVirusContig-6.path.dot
-rw-r--r-- 1 jlin11 users 3.8M Nov  7 16:11 SCNr3_CandidateVirusContig-7.dot
-rw-r--r-- 1 jlin11 users   97 Nov  7 16:11 SCNr3_CandidateVirusContig-7.fa
-rw-r--r-- 1 jlin11 users  172 Nov  7 16:11 SCNr3_CandidateVirusContig-7.path
-rw-r--r-- 1 jlin11 users 3.8M Nov  7 16:11 SCNr3_CandidateVirusContig-8.dot
-rw-r--r-- 1 jlin11 users 7.7M Nov  7 16:11 SCNr3_CandidateVirusContig-8.fa
-rw-r--r-- 1 jlin11 users 651K Nov  7 16:07 SCNr3_CandidateVirusContig-bubbles.fa
lrwxrwxrwx 1 jlin11 users   32 Nov  7 16:10 SCNr3_CandidateVirusContig-contigs.dot -> SCNr3_CandidateVirusContig-6.dot
lrwxrwxrwx 1 jlin11 users   31 Nov  7 16:10 SCNr3_CandidateVirusContig-contigs.fa -> SCNr3_CandidateVirusContig-6.fa
-rw-r--r-- 1 jlin11 users 120K Nov  7 16:08 SCNr3_CandidateVirusContig-indel.fa
lrwxrwxrwx 1 jlin11 users   32 Nov  7 16:11 SCNr3_CandidateVirusContig-scaffolds.dot -> SCNr3_CandidateVirusContig-8.dot
lrwxrwxrwx 1 jlin11 users   31 Nov  7 16:11 SCNr3_CandidateVirusContig-scaffolds.fa -> SCNr3_CandidateVirusContig-8.fa
lrwxrwxrwx 1 jlin11 users   36 Nov  7 16:11 SCNr3_CandidateVirusContig-stats -> SCNr3_CandidateVirusContig-stats.tab
-rw-r--r-- 1 jlin11 users  305 Nov  7 16:11 SCNr3_CandidateVirusContig-stats.csv
-rw-r--r-- 1 jlin11 users  480 Nov  7 16:11 SCNr3_CandidateVirusContig-stats.md
-rw-r--r-- 1 jlin11 users  305 Nov  7 16:11 SCNr3_CandidateVirusContig-stats.tab
lrwxrwxrwx 1 jlin11 users   31 Nov  7 16:08 SCNr3_CandidateVirusContig-unitigs.fa -> SCNr3_CandidateVirusContig-3.fa
```


