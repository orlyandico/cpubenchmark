# cpubenchmark

This is a set of Jupyter notebooks for correlating CPU performance across (many) generations.

- processSpec.ipynb downloads and processes SPECint 2017, 2006, and 2000, cross-correlates, and derives SPECint95. Now you can do a (more or less) apples-to-apples comparison of your fancy Macbook Pro to the Sun Ultra 1 of your youth.

- processSAPS.ipynb downloads and processes the SAP SD2 Tier (Sales and Distribution) benchmark, and attempts to find any correlation between SAPS and SPEC. Spoiler: SAPS SD2 in its current form is basically a CPU benchmark.

TL; DR - you can estimate the SAP SD2 per core for any CPU with a SPECintbase2006 using the formula

**SAPS per Core = (20.57 * SPECintbase2006) + 1061**
