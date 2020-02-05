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
mkdir -p ~/project/fqData/NGS01projectNeveen/bwa_align/bwaIndex && cd ~/project/fqData/NGS01projectNeveen/bwa_align/bwaIndex
ln -s ~/workdir/sample_data/dog_chr5.fa .
bwa index -a bwtsw dog_chr5.fa
```

### Sequence alignment

```
R1="$HOME/workdir/fqData/BD143_TGACCA_L005_R1_001.pe.fq.gz"
R2="$HOME/workdir/fqData/BD143_TGACCA_L005_R2_001.pe.fq.gz"
/usr/bin/time -v bwa mem bwaIndex/dog_chr5.fa $R1 $R2 > BD143_TGACCA_L005.sam
```

### Use a program SAMstat to get statistics on our BD143_TGACCA_L005.sam file

```
cd bwa_align/
