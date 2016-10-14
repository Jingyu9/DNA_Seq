#Create directory

##Under the correct directory /lustre/projects/ to create my own folder 
```
mkdir rawdata
cd rawdata
```
#Download data
##Use the codes from UT austin to download to rawdata into rawdata directory

```
nano gsaf_download.sh

#!/bin/bash
wget -O files.html "$1"
for file in `grep '^<!--gsafdata' files.html | grep '.gz' | awk '{print $2}'`
do
    echo $file
    url=`cat files.html | grep -v json | grep -m 1 $file | awk 'BEGIN {FS="\""} {print $2}'`
    echo "Downloading: $url"
    wget -o $file.wget.log -O $file --no-check-certificate "$url"
done
grep '^<!--gsafdata' files.html | grep '.gz' | awk '{print $5"  "$2}' > md5.txt
numfiles=`wc -l md5.txt | awk '{print $1}'`
md5sum -c md5.txt
if [ $? -eq 0 ]
then
    echo "Downloaded $numfiles files successfully."
else
    echo "Calculated md5sums do not match those provided by the GSAF.  Try requesting a new key and downloading again.  If that fails, contact the GSAF."
fi
```
##Change the file to be excutable
~~~
chmod a+x gsaf_download.sh
~~~
##Run the bash commands on the head node
~~~
./gsaf_download.sh "http://gsaf.access link"
~~~
##Check the integrety of downloaded file
```
ls -lh
tail R1.fastq.gz

```
**There are 
2 fastq.gz files(R1 30G, R2 25G), 
2 fastq.gz.wget.log(for logging the downloading status),
1 files.html (for saving the link info), 
1 md5.txt (for checking the integrety of trasnfering) 
**
#Backup the data
```
mkdir backup
cp *.fastq.gz backup
```


