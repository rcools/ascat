# Processing WES data with ASCAT

The following files have been derived from the reference files in the [Battenberg package](https://github.com/Wedge-lab/battenberg). No filter related to the genomic location was applied so they contain both exonic, intronic and intergenic SNPs. When using such files, one **must** either 1) provide a BED file which defines regions of interest (`BED_file` in `ascat.prepareHTS`) or 2) downsample the files so they are tailored to your sequencing design (option 2 will speed-up ASCAT but only recommended for advanced users). This is because a WES experiment would only cover a small fraction of the genome so we have to provide an exhaustive list of SNPs to start with, considering that only a subset would be covered. As such, reference files for WGS have a lower resolution (there are not meant to be downsampled) and must not be used for processing WES data. Also, because reference files for WES contain an exhaustive list of SNPs, they must not be used for processing WGS. 

Please note that such files can also be used for processing targeted sequencing data (with an appropriate BED file). Since they contain exonic/intronic/intergenic SNPs, they should be applicable to a broad range of designs.

Data availability:

- Loci files: [hg19](https://drive.google.com/file/d/1R2MON6M77kh3M2v7nSOM1_MOEXXnpIbH/view?usp=share_link) & [hg38](https://drive.google.com/file/d/1BqqYUFdQ3uVllBwSkBYs-jrRJFsmB-No/view?usp=share_link) (unzip and set `alleles.prefix="G1000_loci_hg19_chr"` in `ascat.prepareHTS`)
- Allele files: [hg19](https://drive.google.com/file/d/1NtwlPiArWeFaMO1PjuH7aNhhNZ3bMX5J/view?usp=share_link) & [hg38](https://drive.google.com/file/d/101tHEt4r81b-bZxCE50edRXuOCh4bo-M/view?usp=share_link) (unzip and set `loci.prefix="G1000_alleles_hg19_chr"` in `ascat.prepareHTS`)
- GC correction file: [hg19](https://drive.google.com/file/d/1-WZGH0XTtWFjyJV6ucWQ-yaoYtHcztvq/view?usp=share_link) & [hg38](https://drive.google.com/file/d/1-0wOc5woK27tEpUpSNsz0U3xwI-xvBb3/view?usp=share_link) (unzip and set `GCcontentfile="GC_G1000_hg19.txt"` in `ascat.correctLogR`)
- Replication timing correction file: [hg19](https://drive.google.com/file/d/1unad1TkrXV-EFcRM8KBUCXpLXWCIxWyv/view?usp=share_link) & [hg38](https://drive.google.com/file/d/1Etl5HYdC4TNw0oj4AxvbJR_1a1atYBFt/view?usp=share_link) (unzip and set `replictimingfile="RT_G1000_hg19.txt"` in `ascat.correctLogR`)

Please note that loci files provided above are not 'chr'-based (chromosome names are '1', '2', '3', etc. and not 'chr1', 'chr2', 'chr3', etc.). If your BAMs are 'chr'-based, you will need to add 'chr' (Bash: `for i in {1..22} X; do sed -i 's/^/chr/' G1000_loci_hg19_chr${i}.txt; done`). ASCAT will internally remove 'chr' so the other files (allele, GC correction and RT correction) should not be modified and `chrom_names` (`ascat.prepareHTS`) should be `c(1:22,'X')`.