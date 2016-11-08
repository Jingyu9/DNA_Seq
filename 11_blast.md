#Blast the contig result with the viral database

##First, we need to tell blast about our database. BLAST needs to do some pre-work on the database file prior to searching. This helps to make the software work a lot faster. Use the makeblastdb command:
```
makeblastdb -in ../../rawdata/viral_102716.genomic.fna -dbtype nucl
```
write a script (nano blastn.qsh)
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
The result showed most contigs are from phage
only 2 comes from some other virus
```
52075	gi|951885333|ref|NC_028379.1|	94.444	36	1	1	371	406	41839	41805	3.42e-06	54.7	gi|951885333|ref|NC_028379.1| Elephant endotheliotropic herpesvirus 4 isolate North American NAP69, complete genome
59369	gi|584593359|ref|NC_023442.1|	100.000	28	0	0	61	88	8014	8041	5.46e-06	52.8	gi|584593359|ref|NC_023442.1| Buzura suppressaria nucleopolyhedrovirus isolate Hubei, complete genome
```
Each column is labelled as following.


```
   qseqid      Query sequence ID
    sseqid      Subject (ie DB) sequence ID
    pident      Percent Identity across the alignment
    length      Alignment length
    mismatch    # of mismatches
    gapopen     Number of gap openings
    qstart      Start of alignment in query
    qend        End of alignment in query 
    sstart      Start of alignment in subject
    send        End of alignment in subject
    evalue      E-value
    bitscore    Bit score
 ```
    
