# WISE L1b Folded Light Curves of Modified White Dwarf Sample

This folder contains a total of 710 WISE L1b folded light curves from a modified white dwarf sample.

## Usage Recommendations
For catalog purposes, it is advisable to focus on sources with more than 100 data points in either band.

## Source Selection
The white dwarf candidates were sourced from the **Gaia DR2** white dwarf candidate catalog (Gentile Fusillo+, 2019) using the following criteria:

- **Parallax** > 10
- **Proper Motion (PM)** > 0 mas
- **White Dwarf Probability** > 50%

## Matching Procedure
1. **CatWISE Catalog Match:**
   - **Search Radius**: 2 arcseconds (2016 Epoch)
   - **Filters**:
     ```sql
     (cc_flags NOT LIKE 'D___')
     AND (cc_flags NOT LIKE 'H___')
     AND (cc_flags NOT LIKE 'O___')
     AND (cc_flags NOT LIKE 'P___')
     AND (cc_flags NOT LIKE '_D__')
     AND (cc_flags NOT LIKE '_H__')
     AND (cc_flags NOT LIKE '_O__')
     AND (cc_flags NOT LIKE '_P__')
     AND ab_flags = '00'
     AND (
         (w1mpro > 14.5 AND w1snr > 15)
         OR
         (w2mpro > 14.5 AND w2snr > 15)
     )
     ```
   Resulting in 835 sources.

2. **NEOWISE-R Single Exposure (L1b) Source Table Match:**
   - **Criteria**:
     ```sql
     (cc_flags NOT LIKE 'D___')
     AND (cc_flags NOT LIKE 'H___')
     AND (cc_flags NOT LIKE 'O___')
     AND (cc_flags NOT LIKE 'P___')
     AND (cc_flags NOT LIKE '_D__')
     AND (cc_flags NOT LIKE '_H__')
     AND (cc_flags NOT LIKE '_O__')
     AND (cc_flags NOT LIKE '_P__')
     OR cc_flags IS NULL
     AND qual_frame > 4
     AND qi_fact > 0.5
     AND moon_masked = 0
     AND (
         (w1mpro > 14.5 AND w1snr > 15)
         OR
         (w2mpro > 14.5 AND w2snr > 15)
     )
     ```
   - **Finaly**:
     - Unique sources were selected.
     - The search radius was adjusted based on Gaia proper motions, with an additional two years of space. Minimum search radius was set to 5 arcseconds for low PM sources.
     - Sources with fewer than 50 data points were discarded.

## Filtering and Periodogram Analysis

### Position Filtering
- Each data point is cross-checked against the source’s expected position based on Gaia proper motions, with generous 1 arcsecond circle.
- **Top Panels**: Raw data is plotted without additional filters.

### Sigma Clipping for Periodogram
- Data undergoes sigma clipping with parameters: upper = 3, lower = 3.

### Periodogram Settings
- **Period Adjustments**:
  - If the period is close to the WISE interval (~0.066 days) or its fractions, the period is recalculated to avoid aliasing. However aliasing might still occure in some cases.
  - Aliasing fractions are indicated with gray triangles in the **Best Period** figure.
- **Period Range**:
  - Minimum period: 0.5 hours
  - Maximum period: 7 days
- **Execution**: The periodogram is run twice for improved accuracy.
- **Separate Solutions**: Each band is analyzed independently.
