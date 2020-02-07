## Welcome to the NGS01 project repo

### Creating a repository online for the 1st time!
#### Navigate into the folder you want to put on Github
#### Create a file called README.md where you can put instructions/info about your folder

```
$ echo "# Welcome to the NGS01 project repo" > README.md
$ git add README.md 
$ git commit -m "create readme"
```
```
$ git config --global user.email "neveen.abdelaziz@gmail.com"
$ git config --global user.name "NeveenAbdelaziz"
```
```
$ git init # initialize your git repository locally
```
```
$ git add . # adds everything changed from local to staging
```
```
$ git commit -m "first commit" # commits everything in staging to be ready to be pushed to Github
```
```
$ git remote add origin https://github.com/quinnliu/GitCommands.git
```
```
$ git push -u origin master # the "-u" is so that the next time your push you don't need to type "origin master"
```

#### Put in a username & password

### Download reference file

### Install bwa

```
$ conda activate ngs1
$ conda install -c bioconda -y bwa
```

### Index your genome

```
$ mkdir -p ~/project/fqData/NGS01projectNeveen/bwa_align/bwaIndex && cd ~/project/fqData/NGS01projectNeveen/bwa_align/bwaIndex
$ ln -s ~/workdir/sample_data/dog_chr5.fa .
$ bwa index -a bwtsw dog_chr5.fa
```

### Sequence alignment

```
$ R1="$HOME/workdir/fqData/BD143_TGACCA_L005_R1_001.pe.fq.gz"
$ R2="$HOME/workdir/fqData/BD143_TGACCA_L005_R2_001.pe.fq.gz"
$ /usr/bin/time -v bwa mem bwaIndex/dog_chr5.fa $R1 $R2 > BD143_TGACCA_L005.sam
```

### Use samtools flagstat to get mapping statistics

```
samtools flagstat BD143_TGACCA_L005.bam
```
##### 243217 + 0 in total (QC-passed reads + QC-failed reads)
##### 0 + 0 secondary
##### 309 + ##### 0 supplementary
##### 0 + 0 duplicates
##### 239307 + 0 mapped (98.39% : N/A)
##### 242908 + 0 paired in sequencing
##### 121454 + 0 read1
##### 121454 + 0 read2
##### 234716 + 0 properly paired (96.63% : N/A)
##### 235088 + 0 with itself and mate mapped
##### 3910 + 0 singletons (1.61% : N/A)
##### 0 + 0 with mate mapped to a different chr
##### 0 + 0 with mate mapped to a different chr (mapQ>=5)

### Use a program SAMstat to get statistics on our BD143_TGACCA_L005.sam file????????


### Convert SAM file to the binary BAM file

```
$ samtools view -h -b -S BD143_TGACCA_L005.sam > BD143_TGACCA_L005.bam
```

### Extract only those sequences that were mapped against the reference database

```
$ samtools view -b -F 4 BD143_TGACCA_L005.bam > BD143_TGACCA_L005.mapped.bam
```

### Sort BAM file

```
$ samtools sort BD143_TGACCA_L005.mapped.bam -o BD143_TGACCA_L005.mapped.sorted.bam
```

