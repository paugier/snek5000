# Project *eturb*

Efficient simulations of turbulent atmospheric boundary layer.

## Installation

```sh
# Clone
git clone --recursive git@github.com:exabl/eturb.git

# Activate paths: Start here. Always!
cd eturb
source activate.sh

# Build Nek5000
cd lib/Nek5000/tools/
./maketools all
cd -

```

## Workflow

### Easy way

This workflow requires you to setup a python environment. There are two ways to
do this (and it has to be done only once):

1. Using `venv`
   ```sh
   python -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   pip install -e .
   ```
2. Using `conda`
   ```sh
   conda env create -n eturb -f environment.yml
   conda activate eturb
   ```

#### Run Snakemake
```sh
# Everything done via a Snakefile at once
cd src/abl_nek5000/
snakemake run
cd -

# ... or one by one
cd src/abl_nek5000/
snakemake mesh
snakemake compile
snakemake run
snakemake archive
snakemake clean
cd -

```

### Hard way

```sh
# Build case
cd src/abl_nek5000/
CASE="3D_ABL"
echo "$CASE.box" | genbox
mv -f box.re2 3D_ABL.re2
echo "$CASE\n0.01" | genmap
FFLAGS="-mcmodel=medium -march=native" CFLAGS="-mcmodel=medium -march=native" makenek
cd -

# Run case
cd src/abl_nek5000/
nekmpi $CASE <nb_procs> # foreground
nekbmpi $CASE <nb_procs> # background
cd -


# Clean
makenek clean

```

## Development

See [contributing guidelines](CONTRIBUTING.md).
