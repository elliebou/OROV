# OROV

**This is the repository used to build the small, medium, and large segment of Oropouche virus.**

---

This repository contains the steps to use [augur]() to build the OROV dataset. 

## Installation / Set-Up

1. Install [conda](https://conda.io/docs/user-guide/install/index.html)

2. Install augur (and its dependencies) into a conda environment
```bash
git clone git@github.com:nextstrain/augur.git # the nextstrain bioinformatics toolkit
cd augur
conda env create -f environment.yml
export NCBI_EMAIL=<YOUR_EMAIL_HERE>
```
This creates the conda environment `augur` which we must be in for all remaining steps

3. Enable the conda environment
```bash
source activate augur
```

4. Install auspice
```bash
conda install -c conda-forge nodejs
npm install --global auspice
```

4. Clone this repository
```bash
git clone git@github.com:elliebou/JCV-nextstrain.git
cd JCV-nextstrain
```

6. Check augur & auspice are installed:
```bash
augur -h
auspice -h
```

## File Structure
* `Snakefile` - contains the augur / JCV-custom steps to run the build. Each snakemake command can be run as a bash command on it's own, but we use snakemake to simplify things.
* `./data/*` - the input files (private, and not committed to github). You are responsible for creating the two required files here: `./data/full_dataset.fasta` and `./data/headers.csv` (these are referenced in the `Snakefile`).
* `./scripts/*` custom JCV scripts. Called by commands in the `Snakefile.
* `./results/` augur will produce a number of (intermediate) files including the alignment, newick trees etc. Not committed to github.
* `./auspice/` will contain the JSONs necessary for visualisation by auspice.


## Run the build
The `Snakefile` details each step in the buil (See that file for the specifics).
As such, it should be as simple as running
```bash
snakemake clean # remove any files from a previous build
snakemake # run the build pipeline. Takes about 40min
```
and the entire build will run through.


It's worth explaining some of the commands here, many of which are quick and can be re-run on their own to change the output. (For instance, changing colours doesn't require you to re-run the tree building steps.)
