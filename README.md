# VCF Annotation workflow

## Reference files

### 1. Reference fasta and fai
```
wget https://object.genomeinformatics.org/genomics-public-data/reference-genome/GRCh38_hla_decoy_ebv/GRCh38_hla_decoy_ebv.fa
wget https://object.genomeinformatics.org/genomics-public-data/reference-genome/GRCh38_hla_decoy_ebv/GRCh38_hla_decoy_ebv.fa.fai
```

## SNPEFF

### SNPEFF Cache Download (using docker)

#### Download snpeff version used
```
docker pull quay.io/biocontainers/snpeff:5.1--hdfd78af_2
```

#### Identify the newest database version
```
docker run -it quay.io/biocontainers/snpeff:5.1--hdfd78af_2 java -jar /usr/local/share/snpeff-5.1-2/snpEff.jar databases | grep "GRCh38"
```

#### Download the newest database version
```
docker run -v /Users/gfeng/Documents/Work/ICGC-ARGO-WORKFLOWS/VCF_annotation/vcf_annotation/tests/reference/snpeff_cache:/data -it quay.io/biocontainers/snpeff:5.1--hdfd78af_2 java -jar /usr/local/share/snpeff-5.1-2/snpEff.jar download -dataDir /data -v GRCh38.105
```
