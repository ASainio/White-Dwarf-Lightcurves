Here is how positions are retriewed:
1. Sample list of WD candidates
2. Finding candidates with infrared data from CatWISE and L1b tables (epoch 2016)
3. Getting propermotions and epoch 2016 position from GAIA archive
4. Calculating search radius to retrieve all L1b datapoints.
5. Calculating positions to each l1b MJD that should match gaia PM position in given MJD
6. Filtering out sources >1" off the predicted gaia position.
7. Scatter plot filtered data to off-set figure with line where detection should be in given MJD based on Gaia PM.
8. Inspecting off-set by eye.
9. Removed knowns and false positives (galaxies)

These can be systematic, due to parallax, change alignment or close co-mover.

Ideas:
- Check SED for IR excess
- Compare CatWISE PM with GAIA pm (is the L1B source moving)
- If another IR detection is available, like J, then use it to calculate expected Gaia position to same MJD and compare positions.
- High def images?
