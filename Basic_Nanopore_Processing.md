### Concatenating the fastq files
```
cat *fastq.gz > allfiles.fastq.gz
```

### Aligning to reference
```
minimap2 --MD -a "$ref_hg38" allfiles.fastq.gz > mapped.sam
```

### Converting into BAM
```
samtools view -bS mapped.sam > mapped.bam
```

### Sorting
```
samtools sort mapped.bam -o mapped.sorted.bam
```

### Indexing
```
samtools index mapped.sorted.bam
```

### To call structural variants from the sample
```
sniffles -i mapped.sorted.bam -v variants.vcf
sniffles -i mapped.sorted.bam --reference "$ref_hg38" --non-germline -v variants_nongerm.vcf
```

### Annotate using AnnotSV
```
$ANNOTSV/bin/AnnotSV -SVinputFile variants.vcf
```

### Tools for SNV calling
longshot - https://github.com/pjedge/longshot
```
longshot --bam <bam_file> --ref <ref_path> --out <output_file>
```

wf-human-variation-Nextflow pipeline - https://github.com/epi2me-labs/wf-human-variation
Clair3 - https://github.com/HKU-BAL/Clair3
NanoCaller - https://github.com/WGLab/NanoCalle
