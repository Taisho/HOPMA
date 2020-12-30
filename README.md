# HOPMA
HOPMA: a tool to boost protein functonal dynamics with colored contact maps

HOPMA is intended to help to define elastic network representations of protein structures. It takes as input a protein 3D structure and gives as output a set of protein region pairs that should not be connected by any link in the network. HOPMA exploits the protein inter-residue distance matrix. It transforms it into a smoothed binarized colored contact map and detects small contiguous patches in this map. These patches correspond to small contact areas between contiguous protein segments, and the rational is that they indicate contacts that lock the elastic network and hinder its motions. HOPMA's output can be directly given to NOLB: https://team.inria.fr/nano-d/software/nolb-normal-modes/.

### Dependencies:  
HOPMA is implemented in Python and R.
https://www.python.org/
https://cran.r-project.org/  

BIO.PDB and NUMPY Python modules should be installed to be able to use HOPMA.

### Installation:  

Clone the HOPMA repository.  
Install dependencies.  
- for BioPython: pip install Bio  
- for R: brew install r OR brew install --cask r  
Define and export the environment variable *HOPMA_PATH=/path-to-HOPMA-directory/*.  
Test the program on the example PDB file 1dap.pdb, by typing "python3 $HOPMA_PATH/hopma.py 1dap -c B".  
The outputs should be identical to those stored in the *example* directory.  
A help can be accessed by typing "python $HOPMA_PATH/hopma.py --help".  

### Usage notes:  

The protein 3D structure filename in PDB format without the .pdb extension is a mandatory argument.   
You may also give the name of the protein chain you want to analyse ('A' by default).

By default, NOPMA will compute a smoothed contact propensity map using windows of size 5x5 (padding = 2).
It will then use two different contact propensities cutoff values, 0.1 and 0.001, to generate two colored
binarized maps. The output list of excluded contacts is determined by making the union of the small patches
(size lower than 625 cells) detected in the two binarized maps.

HOPMA's outputs are:  
- the CA-CA distance matrix (.dist) in text format,  
- Two colored binarized contact maps (.class) in text format,  
- Two PDF files showing images of the colored binarized contact maps,  
- Three text files (.excl) containing lists of pairs of protein regions that should not be linked by any spring.  
The final result is the "combi" list. This file can be given to NOLB with the option *--excl*.  

### Main reference:  
Laine E, Grudinin S. HOPMA: Boosting protein structures dynamical potential with colored contact maps.*submitted*

