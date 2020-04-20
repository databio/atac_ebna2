# Basic tutorial for running PEPATAC

This tutorial shows you how to run the PEPATAC pipeline on a set of FASTQ files. 

## Clone this repository


```
mkdir pepatac_example
cd pepatac_example
git clone https://github.com/databio/atac_ebna2.git
```

The project config file is a yaml file:

```
cat atac_ebna2.yaml
```

It points to:
 - the sample list (`sample_table`)
 - an output directory (`output_dir`)
 - the pipeline (via the `pipeline_interfaces` key)
 - fastq file locations (the `FQ1` and `FQ2` sources)


Now let's look at the sample table:

```
less -S metadata/atac_ebna2_annotation.csv
```

It's your basic annotation sheet, with one row per sample. 


## Download FASTQ files

Next, download and extract FASTQ files:

```
wget big.databio.org/pepatac/atac_ebna2_fq.tar.gz
tar -xf atac_ebna2_fq.tar.gz
```

## Download the pipeline

Next, clone the PEPATAC pipeline repository:

```
git clone https://github.com/databio/pepatac.git
```


## Run the pipeline

Run the pipeline on each sample using [looper](http://looper.databio.org):

```
PEPATAC=pepatac SRAFQ=fastq looper run metadata/atac_ebna2_config.yaml -d
```

You can populate the PEPATAC and SRAFQ paths as appropriate if you have the pipeline and fastq in different locations. For example:

```
PEPATAC=$HOME/code/pepatac SRAFQ=${SRAFQ} looper run atac_ebna2.yaml -d --package bulker_slurm
```

That's it!
