# Data

The dataset is **not** stored in this repository. The notebook expects a file named
`SDSS_data_galaxies.csv` with columns `objid, ra, dec, z, zErr`.

## How to get it

1. Open the SDSS DR18 SkyServer SQL Search: https://skyserver.sdss.org/dr18/SearchTools/sql
2. Run this query and download the result as CSV:

```sql
SELECT TOP 100000
    p.objid,
    p.ra,
    p.dec,
    s.z,
    s.zErr
FROM SpecObj AS s
JOIN PhotoObj AS p
ON s.bestObjID = p.objID
WHERE
    s.class='GALAXY'
    AND s.zWarning = 0
```

3. Rename the file to `SDSS_data_galaxies.csv`.
   - In Colab: upload it when the first cell asks.
   - Locally: place it in this `data/` folder and change the `read_csv` path accordingly.

Note: `TOP 100000` without `ORDER BY` returns an arbitrary subset, so a re-run may give a slightly
different sample than the one used for the figures in the README.

Data credit: Sloan Digital Sky Survey (SDSS). See https://www.sdss.org/collaboration/citing-sdss/
