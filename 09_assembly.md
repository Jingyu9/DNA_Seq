```
#$ -N abyss
#$ -cwd
#$ -S /bin/bash
#$ -q short*
#$ -l mem=10G,h_vmem=10G
#$ -pe threads 2

module load abyss
abyss-pe k=48 np=2 name=DRR021342 \
in='DRR021342_1.trimmed.paired.fastq DRR021342_2.trimmed.paired.fastq'
```
