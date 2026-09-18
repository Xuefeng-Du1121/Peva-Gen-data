# PEVA-Gen Data

Public data bundle for the PEVA-Gen maritime search-and-rescue simulator.

The release contains regional subsets and demonstration files derived from public NOAA GDP, ECMWF/ERA5, HYCOM, and Copernicus Marine products. It is not a new global dataset and should not be interpreted as field validation of the PEVA-Gen controller.

## Contents

The frozen bundle is under `ocean_system_data_20260913T024902Z/`. Its own `README.md`, `manifest.json`, `SHA256SUMS`, and `runtime-data/demo/provenance.json` describe the source products, variables, spatial and temporal coverage, transformations, and checksums.

Validate the downloaded files from inside the bundle directory:

```bash
sha256sum -c SHA256SUMS
```

Large NetCDF and CSV files are stored with Git LFS. Install Git LFS before cloning or run `git lfs pull` after cloning.

## Important usage notes

- Preserve the original source attribution and product-specific license terms.
- Check time, coordinates, depth, units, missing values, and product provenance before joining files.
- The Copernicus total current must not be added again to current + Stokes + tide components.
- The data are intended for exploration and reproducible simulator inputs; they do not by themselves establish forecast or deployment performance.

The code that consumes this bundle is available at [Peva-Gen](https://github.com/Xuefeng-Du1121/Peva-Gen).

For the formal ocean-field experiments, the surface current field is:

`ocean_system_data_20260913T024902Z/drift-trajectory-system/data_platform/data/raw/environment/copernicus/multobs_currents_east_china_2018_01.nc`

It provides the `total_u` and `total_v` variables expected by `peva_sim.ocean_field.OceanField`.
