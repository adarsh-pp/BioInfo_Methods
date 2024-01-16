#Concatenating the fastq files
```
cat *fastq.gz > allfiles.fastq.gz
```

#Aligning to reference
```
minimap2 --MD -a "$ref_hg38" allfiles.fastq.gz > mapped.sam
```

#Converting into BAM
```
samtools view -bS mapped.sam > mapped.bam
```

#Sorting
```
samtools sort mapped.bam -o mapped.sorted.bam
```

