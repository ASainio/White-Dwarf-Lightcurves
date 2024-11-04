Here is how positions are retriewed:
1. Sample list of WD candidates
2. Retrieved candidates that should have infrared data from CatWISE or NEOWISE L1b tables.
3. Retrieved propermotions and epoch 2016 position from GAIA archive
4. Calculated search radius to retrieve WISE l1b datapoints.
5. Calculated positions for each l1b MJD that should match gaia PM.
6. Removed sources that were >1" away from location where they should be based on GAIA pm.
7. Scatter plotted filtered data to off-set figure and draw line where detection should be in given MJD based on Gaia PM.
8. Inspecting off-set by eye (~20 candidates from ~700 light curves).
9. Removed knowns and false positives (galaxies)

These can be systematic, due to parallax, chance alignment or close co-mover.

Ideas:
- Check SED for IR excess
- Compare CatWISE PM with GAIA pm and check if the scattered data is moving (is the L1B source moving)
- If another IR detection is available (J?), then use it to calculate expected Gaia position to same MJD and compare positions.
- High def images?
