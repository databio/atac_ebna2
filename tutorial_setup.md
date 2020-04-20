# Basic tutorial for running PEPATAC

Assuming you have all the fastq files

Clone PEPATAC

```
git clone https://github.com/databio/pepatac.git
```

Download and extract FASTQ files:

```
wget big.databio.org/pepatac/atac_ebna2_fq.tar.gz
tar -xf atac_ebna2_fq.tar.gz
```

```
PEPATAC=pepatac SRAFQ=fastq looper run metadata/atac_ebna2_config.yaml -d
```

You can populate the PEPATAC and SRAFQ paths as appropriate if you have the pipeline and fastq in different locations. For example:

```
PEPATAC=$HOME/code/pepatac SRAFQ=${SRAFQ} looper run atac_ebna2.yaml -d --package bulker_slurm
```

That's it!