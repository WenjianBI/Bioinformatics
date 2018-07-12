# Bioinformatics
This repository includes usage of some bioinformatics software

## ANNOVAR
Bash files to annotate VCF files based on hg38/hg19 reference assembly.

### Input
- DIR: directory to all output and temporary files
- VCF: input file of .vcf/.vcf.gz, complete directory is required
- PREFIX: prefix for all output and temporary files
NOTE: please update "DIR_DB=/home/wbi1/Bioinformatic-software/ANNOVAR/humandb" if changed.
### Usage
```
./anno4vcf.hg19.sh DIR VCF PREFIX
./anno4vcf.hg38.sh DIR VCF PREFIX
```
