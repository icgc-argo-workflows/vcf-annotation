# VCF Annotation workflow

## Reference files

### 1. Reference fasta and fai
```
wget https://object.genomeinformatics.org/genomics-public-data/reference-genome/GRCh38_hla_decoy_ebv/GRCh38_hla_decoy_ebv.fa
wget https://object.genomeinformatics.org/genomics-public-data/reference-genome/GRCh38_hla_decoy_ebv/GRCh38_hla_decoy_ebv.fa.fai
```
Move the fasta and fai file under repository `tests/reference`

The path to fasta file is configured in `config/test.config`.

### 2.SNPEFF Cache
It is optional to download snpeff cache. Benefits of cache download include saving pipeline running time and option to run offline. The currently pipeline is designed to have cache downloaded before running the pipeline. In current nf-core SNPEFF module, the version used is snpeff:5.1. Follow the following steps to download the newest database version of snpeff:5.1. 

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
Move the GRCh38.105/ cache directory under `tests/reference`

The path to SNPEFF Cache is configured in `config/test.config`.

### 3. VEP Cache
```
wget https://ftp.ensembl.org/pub/release-112/variation/indexed_vep_cache/homo_sapiens_merged_vep_112_GRCh38.tar.gz
```
Move the .tar.gz file under `tests/reference/vep_cache/homo_sapiens/112/GRCh38` 

The path to VEP Cache is configured in `config/test.config`.

## Usage
1. download reference fasta, SNEEFF Cache and VEP Cache. Place them in the correct path or configure them accordingly.
2. Retrive API token.
3. Command
   ```
   nextflow run main.nf -profile docker,rdpc_qa,test_rdpc_qa,test --study_id TCRB-CA --analysis_id 14d77bd5-e14d-4dd3-977b-d5e14dedd3fb --api_token XXXXX --tools_to_use ensemblvep,snpeff
   ```

