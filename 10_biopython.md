##Use biopython to work on the contig

write (nano readContig.py)
```
from Bio import SeqIO

fasta_file = open("../9_assembly/SCNr3_CandidateVirusContig-scaffolds.fa")
for seq_record in SeqIO.parse(fasta_file, "fasta") :
        print(seq_record.id)
        print(str(seq_record.seq))
        print(len(str(seq_record.seq)))
        print("---------")
fasta_file.close()
```
Then run python
```
module load python (or change version to python 3: module switch python )
python readContig.py
```
This will print all the sequence information to the screen

Another script (nano sortContigs.py)
```
from Bio import SeqIO

result_file = open("sorted_CandidateVirusContig.fasta","w")

records = list(SeqIO.parse("../9_assembly/SCNr3_CandidateVirusContig-contigs.fa","fasta"))
records.sort(cmp=lambda x,y: cmp(len(y),len(x)))
SeqIO.write(records, "sorted_CandidateVirusContig.fasta", "fasta")

#fasta_file.close()
result_file.close()
```
This generated SCNr3_CandidateVirusContig-contigs.fa with the longest sequence at the beginning position




