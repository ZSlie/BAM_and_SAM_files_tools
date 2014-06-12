## Unmapped Reads in a Samfile

Please take note, you should have a [BEOCAT account](http://support.cis.ksu.edu/BeocatDocs/GettingStarted) or [samtools downloaded](http://sourceforge.net/projects/samtools/files/latest/download) for this exercise.

#### Part 1:

#### Part 2:
Filter SAM files to create file with only unmapped reads using the Samtools flag filter.

```
/homes/bioinfo/bioinfo_software/samtools-0.1.18/samtools view -S -f4 /homes/bioinfo/test_de_novo_DE/BT20_rep1_200.sam > ~/unmapped/BT20_rep1_200.unmapped.sam
```
Read more on flag [here](http://picard.sourceforge.net/explain-flags.html.).
Read more on samtools [here](http://samtools.sourceforge.net/samtools.shtml#3.).

#### Part 3:
Convert SAM to fastq
```
java -jar ~/bioinfo_software/picard-tools-1.112/SamToFastq.jar INPUT=/homes/bioinfo/unmapped/BT20_rep1_200.unmapped.sam FASTQ=/homes/bioinfo/unmapped/BT20_rep1_200.unmapped_1.fastq SECOND_END_FASTQ=/homes/bioinfo/unmapped/BT20_rep1_200.unmapped_2.fastq
```
Read more on picard [here](http://picard.sourceforge.net/).

###### Note:
Picard-tools-1.112 does not like relative paths so use the absolute path in file names.

e.g.
```
/homes/jfellers/unmapped/filename
``` 
rather than 
```
"~/unmapped/filename" 
```

#### Part 3:
Check for broken pairs
This simple script, broken_pair_removal.pl, finds pairs that have been broken and moves them to a separate file as single end reads. The script takes the full path of your forward and reverse reads followed by full path of your forward and reverse read output files.
```
perl /homes/sheltonj/abjc/scripts/broken_pair_removal.pl /homes/bioinfo/unmapped/BT20_rep1_200.unmapped_1.fastq /homes/bioinfo/unmapped/BT20_rep1_200.unmapped_2.fastq /homes/bioinfo/unmapped/BT20_rep1_200.unmapped_2_bp.fastq /homes/bioinfo/unmapped/BT20_rep1_200.unmapped_2_bp.fastq
```

