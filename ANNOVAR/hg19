#!/bin/bash

## NOTE: WE UNIFORMLY USE HG19. FOR LIFTOVER, WE SUGGEST "CROSSMAP" SOFTWARE.

if (($#==0))
then
echo "/home/wbi1/Pipeline_BWJ/ANNOTATION_hg19.sh DIR VCF PREFIX"
exit
fi

module load vcftools/0.1.13
module load annovar/030717

DIR=$1     # directory to all output and temporary files
VCF=$2     # input .vcf OR .vcf.gz files, should include directory
PREFIX=$3  # prefix for all output and temporary files
DIR_DB=/home/wbi1/Bioinformatic-software/ANNOVAR/humandb

if (($#==4)) # if there are 4 argumenets, that should be argument to extract bed files
then
BED=$4  # -protocol bed,bed,bed,bed -operation r,r,r,r -nastring . -bedfile GATA1_merged.bed,GATA1_merged.overlap_motif.bed,GATA1_motif.GRCh38.bed,ErySpecificRegions.hg38.bed -arg '-colsWanted 4','-colsWanted 4','-colsWanted 4',''
fi

## STEP 1. CREATE DIRECTORY AND CHANGE THE CURRENT DIRECTORY

mkdir ${DIR}
cd ${DIR}


## STEP 2. GENERATE ANNOVAR INPUT BASED ON VCF FILE

convert2annovar.pl -format vcf4 ${VCF} -outfile ${PREFIX}.tmp.av -allsample -withfreq   # CREATE POSITION ROWS OF ANNOVAR FORMAT
cat ${VCF} | grep -v "^#" | cut -f 2,4,5 > ${PREFIX}.tmp.pos                            # RETAIN ORIGINAL VCF FILE POSITION
paste ${PREFIX}.tmp.av ${PREFIX}.tmp.pos > ${PREFIX}.tmp.avinput                        # PASTE THE ABOVE TWO FILES
cat ${PREFIX}.tmp.avinput | cut -f 1-5,9,10,11 > ${PREFIX}.avinput                      # REMOVE UNIMPORTANT COLUMNS
rm ${PREFIX}.tmp.avinput ${PREFIX}.tmp.pos ${PREFIX}.tmp.av                             # REMOVE TEMP FILES


## STEP 3. TYPYCAL ANNOTATION WITH ANNOVAR SOFTWARE

table_annovar.pl ${PREFIX}.avinput ${DIR_DB} -out ${PREFIX}.anno -build hg19 -remove -protocol refGene,cytoBand,avsnp147,gwasCatalog -operation g,r,f,r -nastring . -otherinfo

if (($#==4))
then
table_annovar.pl ${PREFIX}.avinput ${DIR_DB} -out ${PREFIX}.bed -build hg19 -remove ${BED} 
paste ${PREFIX}.anno.hg38_multianno.txt ${PREFIX}.bed.hg38_multianno.txt > ${PREFIX}.complete
fi

## minor modification for header
# cat pasted_multianno.txt | cut -f 1-14,20-23 | sed -e '1s/bed/GATA1_merged/1' -e '1s/bed2/GATA1_merged.overlap/1' -e '1s/bed3/GATA1_motif/1' -e '1s/bed4/ErySpecificRegions/1' > chr$chr.hg38.complete 


