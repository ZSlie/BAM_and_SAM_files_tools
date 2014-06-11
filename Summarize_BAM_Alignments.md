## Summarize BAM Alignments

Please take note, you should have a [BEOCAT account](http://support.cis.ksu.edu/BeocatDocs/GettingStarted) or [samtools downloaded](http://sourceforge.net/projects/samtools/files/latest/download) for this exercise.

All of the scripts you will need to complete this lab as well as the sample data set will be copied to your Beocat directory as you follow the instructions below. You should type or paste the text in the beige code block into your terminal as you follow along with the instructions below. If you are not used to command line, practice with real data is one of the best ways to learn.

If you would like a quick primer on basic linux commands try [these 10 minute](http://software-carpentry.org/v4/shell/index.html) lessons from Software Carpentry. To learn to start using Beocat and begin using the terminal go to https://github.com/i5K-KINBRE-script-share/FAQ/blob/master/UsingBeocat.md. Learn how to download files from Beocat at https://github.com/i5K-KINBRE-script-share/FAQ/blob/master/BeocatEditingTransferingFiles.md.

#### Part 1:
Retrieve files from my directory for personal use.

```
ln -s /homes/sliefert/Summarize_Bam_Example/Sort.bam ~/Your_folder/
```

The ~/ is a [relative path](http://www.physics.utah.edu/~detar/lessons/unix_intro/unix_intro/node2.html), the equivalent is your home directory. 

Let's create one more symbolic link, we'll need it for the excercises below.

```
ln -s /homes/sliefert/Summarize_Bam_Example/acceptedHits.bam ~/Your_folder/
```
[More reading on symbolic links.](http://www.cyberciti.biz/faq/unix-creating-symbolic-link-ln-command/)

#### Part 2:
Concatenate BAM or SAM files using the samtools cat tool. 
Here is a usage statement for `samtools cat`
```
Usage: samtools cat [-h header.sam] [-o out.bam] <in1.bam> <in2.bam> [...]
```

```
/homes/bioinfo/bioinfo_software/samtools/samtools cat -o /homes/sliefert/Summarize_Bam_Example/outputFile.bam /homes/sliefert/Summarize_Bam_Example/Sort.bam /homes/sliefert/Summarize_Bam_Example/acceptedHits.bam
```

Let's walk through this example.
We start by calling samtools software with:
```
/homes/bioinfo/bioinfo_software/samtools/samtools
```
Then, the concatenate command is ran with
```
cat -o
```
The -o points to what the output file will be.

The next step is to link the output file, that is done with
```
/homes/sliefert/Summarize_Bam_Example/outputFile.bam
```
Finally we take any bam files that we wish to concatenate 
```
/homes/sliefert/Summarize_Bam_Example/Sort.bam  /homes/sliefert/Summarize_Bam_Example/acceptedHits.bam
```
###### Note:
A space separated the list of the bam files you want to merge, USE THEIR FULL PATH.

Additional reading on samtools can be found [here](http://samtools.sourceforge.net/samtools.shtml).


#### Part 3:
Now, we use samtools flagstat to summarize alignments metrics.

```
/homes/bioinfo/bioinfo_software/samtools/samtools flagstat /homes/sliefert/Summarize_Bam_Example/Sort.bam
```
Here is sample output for this command:
```
90061 + 0 in total (QC-passed reads + QC-failed reads)
0 + 0 duplicates
90061 + 0 mapped (100.00%:-nan%)
90061 + 0 paired in sequencing
34615 + 0 read1
55446 + 0 read2
9689 + 0 properly paired (10.76%:-nan%)
65429 + 0 with itself and mate mapped
24632 + 0 singletons (27.35%:-nan%)
2836 + 0 with mate mapped to a different chr
150 + 0 with mate mapped to a different chr (mapQ>=5)
```
Flagstat is a command for summary statistics; you can read more on how to interpret those statistics [here](http://picard.sourceforge.net/explain-flags.html).
