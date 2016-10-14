##Create Analysis directory under my project directory
```
mkdir analysis
cd analysis
mkdir 1_fastqc
```
##Run fastqc in the interactive mode
```
qrsh # request the working node
# Then change to the correct directory
module load fastqc 
which fastqc # showing the current used version of fastqc

fastqc -t 2 -o . ../../rawdata/JLSCNr3_S99_L005_R1_001.fastq.gz
fastqc -t 2 -o . ../../rawdata/JLSCNr3_S99_L005_R2_001.fastq.gz
```
#Result
**Generate 2 fastqc.zip (~300k) and 2 fastqc.html (~250k)**
**Open the .html file and read the result**
**Basic Statistics
Measure	Value
Filename	| JLSCNr3_S99_L005_R1_001.fastq.gz
File type	| Conventional base calls
Encoding	| Sanger / Illumina 1.9
Total Sequences |	304730696
Sequences flagged as poor quality	| 0
Sequence length |	151
%GC	| 38
**
