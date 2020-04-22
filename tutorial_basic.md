# Basic tutorial for running PEPATAC

This tutorial shows you how to run the PEPATAC pipeline on a set of FASTQ files. It assumes you have already installed the prerequisite pipeline software, such as [looper](http://looper.databio.org), and all software required by [pepatac](http://pepatac.databio.org), which is not covered in this tutorial.

## Clone this repository

```
mkdir pepatac_example
cd pepatac_example
git clone https://github.com/databio/atac_ebna2.git
cd atac_ebna2
```

The project config file is a yaml file:

```
cat atac_ebna2.yaml
```

It points to:
 - the sample list (`sample_table`)
 - an output directory (`looper` section, `output_dir`)
 - the pipeline (via the `pipeline_interfaces` key)
 - fastq file locations (the `FQ1` and `FQ2` sources)


Now let's look at the sample table:

```
less -S metadata/atac_ebna2_annotation.csv
```

It's a basic annotation sheet, with one row per sample. This metadata has been populated directly from [GEO for this dataset](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE148396).


## Download FASTQ files

Next, download and extract FASTQ files:

```
cd ..
wget http://big.databio.org/example_data/GSE148396_ATAC_fastq.tgz
# ln -s /project/bioc8145/week5/GSE148396_ATAC_fastq.tgz  GSE148396_ATAC_fastq.tgz
tar -xf GSE148396_ATAC_fastq.tgz
```

## Download the pipeline

Next, clone the PEPATAC pipeline repository:

```
git clone --branch cfg2 https://github.com/databio/pepatac.git
```

You can run the pipeline on an individual sample by just running it as a python script:

```
./pepatac/pipelines/pepatac.py --help
```

## Run the pipeline

Run the pipeline on each sample using [looper](http://looper.databio.org):

```
PEPATAC=`pwd`/pepatac SRAFQ=project/shefflab/data/sra_fastq PROCESSED=output looper run atac_ebna2/atac_ebna2.yaml -d
```

You can populate the PEPATAC and SRAFQ paths as appropriate if you have the pipeline and fastq in different locations. For example:

```
PEPATAC=$HOME/code/pepatac SRAFQ=${SRAFQ} looper run atac_ebna2.yaml -d --package bulker_slurm
```

That's it!
