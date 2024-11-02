This folder consist total of 710 WISE l1b folded lightcurves of modified White Dwarf sample.
- For catalog use it is advisable to use sources with >100 datapoints on either band.


Sources are from Gaia DR2 white dwarf candidates (Gentile Fusillo+, 2019)

-Search criteria:
-Parallax > 10
-PM > 0 mass
-Probability of being WD > 50%

Then source catalogs 2016 epoch is matched to CatWISE catalog with following parameters:
- Search radius 2" matching 2016 epochs:
- 
        (cc_flags NOT LIKE 'D___') 
        AND (cc_flags NOT LIKE 'H___') 
        AND (cc_flags NOT LIKE 'O___') 
        AND (cc_flags NOT LIKE 'P___') 
        AND (cc_flags NOT LIKE '_D__') 
        AND (cc_flags NOT LIKE '_H__') 
        AND (cc_flags NOT LIKE '_O__') 
        AND (cc_flags NOT LIKE '_P__') 
        AND ab_flags = '00'
    )
    AND (
        (w1mpro > 14.5 AND w1snr > 15)
        OR 
        (w2mpro > 14.5 AND w2snr > 15)
    );


(Resulting 835 sources).

Then the same input file is matched to NEOWISE-R Single Exposure (L1b) Source Table:
    (
        (
            (cc_flags NOT LIKE 'D___') 
            AND (cc_flags NOT LIKE 'H___') 
            AND (cc_flags NOT LIKE 'O___') 
            AND (cc_flags NOT LIKE 'P___') 
            AND (cc_flags NOT LIKE '_D__') 
            AND (cc_flags NOT LIKE '_H__') 
            AND (cc_flags NOT LIKE '_O__') 
            AND (cc_flags NOT LIKE '_P__')
        )
        OR cc_flags IS NULL
    )
    AND qual_frame > 4
    AND qi_fact > 0.5
    AND moon_masked = 0
    AND (
        (w1mpro > 14.5 AND w1snr > 15)
        OR
        (w2mpro > 14.5 AND w2snr > 15)
    );

- Unique sources are then picked for input.
- Search radius is calculated using GAIA proper motions and extra 2 years of movement is added. Minimun search radius =5"
- Sources need to have more than 50 datapoints on either band after filtering or they get discarded.


Filtering:
- Each datapoint is compared to position where source should be in given time based on Gaia proper motions with generous 1" circle.
- Raw data is plotted without other filters to to top panels.
- For periodogram data is being sigma clipped, upper=3, lower=3.
  
  Periodogram settings:
  - If period is close to WISE intervall ~0.066d or it's fractions it recalculates new period. This however affects only to lower periods and aliasing by 0.066 can still happen.
  - Aliasing fractions are indicate with krey triangle in Best Period figure.
  - Minimum period: 0.5hours
  - Maximum period: 7 days
  - Periodogram is ran twice for best accuracy.
  - Solutions are ran separatly for each band.
