#Blast the contig result with the viral database


```
#$ -N blastn
#$ -q medium*
#$ -cwd
#$ -pe threads 8
#$ -S /bin/bash
module switch intel-compilers/2016u3
module load blast
blastn \
-query ../10_biopython/sorted_CandidateVirusContig.fasta \
-db ../../rawdata/viral_102716.genomic.fna \
-out Contig_vs_Virus_blastn_results.THREADED.tab \
-evalue 1e-5 \
-outfmt "6 std stitle" \
-num_threads 8
```

