# Bioinformatics
This repository includes usage of some bioinformatics software

## Bad interpreter  
This issue happens a lot when creating scripts in Windows env and then porting over to run on a Unix environment.
```
sed -i -e 's/\r$//' scriptname.sh
```

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

### Imputation related
[Michigan imputation Server](https://imputationserver.sph.umich.edu/index.html#!pages/home) is well developted to impute data for more genome coverage.
- Please remember to select the closest reference panel based on the study samples population
- Will Rayner provides a great toolbox to prepare data for imputation: [HRC preparation checking Tool](http://www.well.ox.ac.uk/~wrayner/tools/)
- R2 greater than 0.3 is a widely used filter. The below is an example code.
```
module load vcflib/051916
vcffilter -f "R2 > 0.3" -f "MAF < 0.05" input_vcfgz > output_vcf  
```
