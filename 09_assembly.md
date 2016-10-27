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
