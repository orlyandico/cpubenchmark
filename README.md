# cpubenchmark

This is a set of Jupyter notebooks for correlating CPU performance across (many) generations.

TL; DR

- you can estimate the SAP SD2 per core for any CPU with a SPECintbase2006 with the formula **SAPS per Core = (20.57 * SPECintbase2006) + 1061**

- you can estimate the SAPS for a given system with a SPECintrate2006 with the formula **SAPS = (54.8 * SPECintrate2006) + 5765**

- **processSpec.ipynb** downloads and processes SPECint 2017, 2006, and 2000, cross-correlates, and derives SPECint95. Now you can do a (more or less) apples-to-apples comparison of your fancy Macbook Pro to the Sun Ultra 1 of your youth. This notebook writes a CSV file that is needed by the second notebook.

- **processSAPS.ipynb** downloads and processes the SAP SD2 Tier (Sales and Distribution 2-tier) benchmark, which is a generally accepted "enterprise workload" benchmark. The notebook attempts to find any correlation between SAPS and SPEC by fuzzy-matching systems from the SPEC benchmark summary, and the SAPS benchmark summary. Spoiler: SAP SD2 in its current form is basically a CPU benchmark.

The second two notebooks attempt to correlate SAPS with the SPECintrate, which is a more natural comparison because SAPS is a whole-system benchmark and SPECrate is a throughput benchmark.  The artificial "SAPS per core" of the above is not very accurate because SAPS does not scale linearly as you add more cores to a system.

- **processSpecRate.ipynb** downloads and processes SPECrate 2017, 2006, and 2000, cross-correlates and writes a CSV file. This is needed by the second notebook.

- **processSAPS_specrate.ipynb** downloads and processes the SAP SD2 Tier (Sales and Distribution 2-tier) benchmark, which is a generally accepted "enterprise workload" benchmark. The notebook attempts to find any correlation between SAPS and SPECrate by fuzzy-matching systems from the SPEC benchmark summary, and the SAPS benchmark summary. We try a polynomial fit (spoiler: linear fit is best) although better results can be obtained using a random forest predictor. This notebook also outputs a Pickle file containing the trained model.

- **consume_SPEC_to_SAPS.ipynb** loads the Pickle model and demonstrates how to predict SAPS from SPEC

The formula however badly over-estimates SAPS for really old machines (a machine with a SPECintrate2006 of zero would still report 5765 SAPS). The random forest algorithm badly under-estimates SAPS for very large machines (e.g. Fujitsu M10-4S which has 13625 SPECintrate2006) and also over-estimates SAPS for really old machines, although to a lesser degree than the linear regression.

Both algorithms give very good fits for systems with SPECintrate2006 between 70 and 2000, which corresponds to the numerous Intel Xeon systems used to train the model.
