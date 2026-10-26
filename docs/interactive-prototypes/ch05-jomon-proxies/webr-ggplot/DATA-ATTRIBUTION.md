# Figure 3 plotting summaries — attribution and provenance

Source: Enrico R. Crema and Ken’ichi Kobayashi (2020), Journal of Archaeological Science 117:105136. https://doi.org/10.1016/j.jas.2020.105136

Fixed author repository: https://github.com/ercrema/jomonPhasesAndPopulation/tree/v.3.0 ; commit a9608543856c3bf22fd94a682ea47e2952c6e1bd. Zenodo: https://doi.org/10.5281/zenodo.4308578.

Licence: author repository README identifies CC BY 3.0, https://creativecommons.org/licenses/by/3.0/ . Retain attribution, licence, source, and changes. This does not grant rights to separate third-party materials.

Educational transformation: three 50-row, 100-cal-BP-bin plotting summary tables exported from author saved RData caches, without rerunning OxCal or the 5000 original simulations.

- Panel a: simdatesPithouses.RData (tblocks.trap, tbs2): calBP, mean, lower, upper.
- Panel b: spdRes.RData (spdDataSPD_blocks$sumblock): calBP, spd.
- Panel c: comp.RData (tblockRoll10.trap): calBP, mean, lower, upper.

The lower/upper values are empirical 2.5%/97.5% simulation quantiles, not automatically frequentist confidence intervals. calBP denotes 100-year bin centres from 7950 to 3050. SPD is a calibrated summed probability density, not a raw radiocarbon-age histogram.

Third-party provenance: housing analysis draws on Suzuki (2006). This minimal package does not reproduce Suzuki's five original housing CSVs or complete RData caches.

Reproduce: run figure3-ggplot2.R on the author's fixed v3.0 checkout; run prepare_data.py on the resulting CSV directory; then run validate_release_data.py. manifest.json records SHA-256 checksums and row counts. Do not manually alter exported CSVs.

Release status: the three CSVs are generated and checked on the user's Mac; this attribution file does not imply that the data files have already been committed or deployed.
