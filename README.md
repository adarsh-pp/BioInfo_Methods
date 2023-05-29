# Bioinformatics_tools

### Converting BAM to Fastq

#### Using bazam (https://github.com/ssadedin/bazam) and BBMap (https://jgi.doe.gov/data-and-tools/software-tools/bbtools/bb-tools-user-guide/bbmap-guide/)
# Converting bam to an interleaved FASTQ format( a type of FASTQ file that contains both the forward and reverse reads of a paired-end fragment in a single file)
java -jar bazam.jar -bam input.bam > output.fastq
#Splitting the file into read one and read two (https://www.biostars.org/p/426628/)
bash //reformat.sh in=original.fq out1=R1.fq out2=R2.fq

##### Using Samtools and Bedtools (https://www.metagenomics.wiki/tools/samtools/converting-bam-to-fastq)

######Sorting the BAM file 
samtools sort -n input.bam -o input_sorted.bam   # sort reads by identifier-name (-n)
######Generating read one and read two fastq files from the sorted BAM
bedtools bamtofastq -i input_sorted.bam -fq output_r1.fastq -fq2 output_r2.fastq
