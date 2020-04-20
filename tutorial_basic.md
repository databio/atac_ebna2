# Basic tutorial for running PEPATAC

This tutorial shows you how to run the PEPATAC pipeline on a set of FASTQ files. 

## Download FASTQ files

First, download and extract FASTQ files:

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