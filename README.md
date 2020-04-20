# ATAC EBNA2 project


The `metadata/atac_ebna2_config.yaml` file is the working PEP for these samples.
The `metadata/atac_ebna2_annotation.csv` file is the working annotation file for these samples.

## Download data

Get source samples using geofetch
```
cd code/atac_ebna2
geofetch -i sample_gsm_list.txt -n atac_ebna2 -u metadata --just-metadata
geofetch -i sample_gsm_list.txt -n atac_ebna2 -u metadata
```

You can set up a default sratoolkit config like this:

```
export DATA="..."
echo "/repository/user/main/public/root = \"$DATA\"" > ${HOME}/.ncbi/user-settings.mkfg
```

## Format your PEP

Validate the configuration file with [`eido`](https://github.com/pepkit/eido) like so:

```
eido validate -p metadata/atac_ebna2_config.yaml -s http://schema.databio.org/pep/2.0.0.yaml
```



```
eido validate -p metadata/atac_ebna2_config.yaml -s http://schema.databio.org/pipelines/pepatac.yaml
```

## Convert the SRA files to FASTQ

Use the `sra_convert` amendment to point at the conversion pipeline. Run in looper:
```
looper run paqc.yaml --amendments sra_convert --lump 25
```

## Run PEPATAC

```
PROCESSED=/project/shefflab/processed DATA=/project/shefflab/data/ looper run paqc.yaml -d
```

The `peppro_paper.yaml` file is the working PEP for these samples.
The `peppro_paper.csv` file is the working annotation file for these samples.
