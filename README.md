# MSCquartets-parallel

# TL;DR

This will speed up species tree/network estimation in ~linear proportion to the number of CPUs available to you, if you are using the R package MSCquartets.

# Dependencies

R >= 3.2.0

R packages MSCquartets, future.apply

# Deets

The recently developed R package MSCquartets (Jones et al. 2020) implements several algorithms for (network) multispecies coalescent-based species tree/network estimation, all of which seem to depend on the `quartetTable()` function, which loops over gene trees and counts quartet frequencies. The number of quartets for a given tree is n [choose] 4, which increases exponentially. The script here `Parallel_quartetTable_byTree.R` encodes `Parallel_quartetTable_byTree()` which uses the future.apply package to parallelise quartet counting by tree and then sums up the quartet frequencies to make a table identical to that generated by the original function. `Parallel_NANUQ.R` contains the aforementioned function and the function `Parallel_NANUQ()` which makes use of it (the actual NANUQ algorithm is unchanged). 

# Additional arguments
RAM_Gigs=1 ; any real number, specifying the memory limit per core in gigabytes (for large trees, a lot of memory might be required; I've found 5 Gigs to work fine for <= 80-taxon trees)

parallel=TRUE (not available in `Parallel_NANUQ()`);  if FALSE, it uses `sapply()` instead of `future_sapply()` which seems to actually be a little slower than the original function (not sure why)

# References and links
https://cran.r-project.org/web/packages/MSCquartets/index.html
https://cran.r-project.org/web/packages/future.apply/index.html

MSCquartets 1.0: Quartet methods for species trees and networks under the multispecies coalescent model in R
John A. Rhodes, Hector Baños, Jonathan D. Mitchell, Elizabeth S. Allman
bioRxiv 2020.05.01.073361; doi: https://doi.org/10.1101/2020.05.01.073361

Allman, E.S., Baños, H. & Rhodes, J.A. NANUQ: a method for inferring species networks from gene trees under the coalescent model. Algorithms Mol Biol 14, 24 (2019). https://doi.org/10.1186/s13015-019-0159-2

Bengtsson, H., 2018. future. apply: Apply function to elements in parallel using futures.
