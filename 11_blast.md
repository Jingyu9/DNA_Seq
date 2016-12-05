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
    
##In 6.2 assembly folder, new contigs were assembled before mapping to viral genomes.
Using tblastx (tblastx_2.qsh, 2 means to use the assemblefirst contigs) to blast these contigs with Viral genomes to identify the candidate contigs
```
#$ -N tblastx
#$ -q medium*
#$ -cwd
#$ -pe threads 8
#$ -S /bin/bash
module switch intel-compilers/2016u3
module load blast
tblastx \
-query ../6.2_assembly/SCNr3_consensus-contigs.fa \
-db ../../rawdata/viral_102716.genomic.fna \
-out Contig_vs_Virus_tblastx_results_2.THREADED.tab \
-evalue 1e-5 \
-outfmt "6 std stitle" \
-num_threads 8
```
the output should include the following information
 qseqid means Query Seq-id
               qgi means Query GI
              qacc means Query accesion
           qaccver means Query accesion.version
              qlen means Query sequence length
            sseqid means Subject Seq-id
         sallseqid means All subject Seq-id(s), separated by a ';'
               sgi means Subject GI
            sallgi means All subject GIs
              sacc means Subject accession
           saccver means Subject accession.version
           sallacc means All subject accessions
              slen means Subject sequence length
            qstart means Start of alignment in query
              qend means End of alignment in query
            sstart means Start of alignment in subject
              send means End of alignment in subject
              qseq means Aligned part of query sequence
              sseq means Aligned part of subject sequence
            evalue means Expect value
          bitscore means Bit score
             score means Raw score
            length means Alignment length
            pident means Percentage of identical matches
            nident means Number of identical matches
          mismatch means Number of mismatches
          positive means Number of positive-scoring matches
           gapopen means Number of gap openings
              gaps means Total number of gaps
              ppos means Percentage of positive-scoring matches
            frames means Query and subject frames separated by a '/'
            qframe means Query frame
            sframe means Subject frame
              btop means Blast traceback operations (BTOP)
            staxid means Subject Taxonomy ID
          ssciname means Subject Scientific Name
          scomname means Subject Common Name
        sblastname means Subject Blast Name
         sskingdom means Subject Super Kingdom
           staxids means unique Subject Taxonomy ID(s), separated by a ';'
                         (in numerical order)
         sscinames means unique Subject Scientific Name(s), separated by a ';'
         scomnames means unique Subject Common Name(s), separated by a ';'
        sblastnames means unique Subject Blast Name(s), separated by a ';'
                         (in alphabetical order)
        sskingdoms means unique Subject Super Kingdom(s), separated by a ';'
                         (in alphabetical order)
            stitle means Subject Title
        salltitles means All Subject Title(s), separated by a '<>'
           sstrand means Subject Strand
             qcovs means Query Coverage Per Subject
           qcovhsp means Query Coverage Per HSP
            qcovus means Query Coverage Per Unique Subject (blastn only)
            
such as
480	gi|9625564|ref|NC_001343.1|	42.667	75	43	0	2	226	5955	6179	1.92e-13	74.5	gi|9625564|ref|NC_001343.1| Commelina yellow mottle virus, complete genome
480	gi|998745916|ref|NC_029303.1|	39.474	76	46	0	2	229	5606	5833	6.79e-13	72.6	gi|998745916|ref|NC_029303.1| Blackberry Virus F isolate BBV-3X, complete genome


