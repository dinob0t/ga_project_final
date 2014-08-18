# Investigating the relationship between solar magnetic activity and coronal mass ejections

## Summary

An coronal mass ejection (CME) is an energetic event in which the sun ejects a large body of plasma along with a frozen in magnetic field configuration into the solar wind. A so called 'halo' event occurs when this ejection appears primarily along the Earth-Sun field of view. It is these events in particular which pose risk to Earth because of the strong association with space weather and geomagnetic storms arising from the CME's magnetic interaction with the Earth's magnetic field. This poses problems for astronauts, satellites, high frequency communications, and may induce currents in any long conductors near the Earth's poles (pipelines, powerlines etc.) It is clearly of interest to understand and predict these events.

Because of the strong association of CMEs and the solar magnetic field configuration, a natural place to start looking at predictors is the sun spot cycle (sun spots occur because the twisted magnetic configurations inhibit heat convection and hence the plasma cools appearing dark, especially in hydrogen-alpha line images of the sun). Excellent data on sun spot numbers exists as far back as the 1800s, and more recently the latitude and longitude of sun spot areas on the sun is documented daily. Other indicators of solar activity include the solar irradiance or radio flux (akin to the power output of the sun) which can be observed at the Lyman Alpha line or 10.7cm Hydrogen line, respectively.  Even better are the vector magnetograms that directly image the magnetic field configuration on the sun's surface for which we have images produced every 15 minutes since 2010. Furthermore to train our classifiers we have the LASCO catalogue of CMEs which has documented every (observerable/detectable) CME since 1997.

## Project files
`cmes.ipynb` - looks at the association of more qualitative sun activity measures on predicting CMEs.
`magnetograms.ipynb` - uses vector magnetogram data from 2010-2013 to analyse solar activity and attempt to predict CMEs.

## Data
`issn.md` - international sunspot number record
`daily_area.txt` - daily area of the sun covered in sunspots
`lyman_alpha.txt` - daily solar irradiance
`f10.7.txt` - daily radio flux
`g*.txt` - Greenwich sunspot grouping data (tracks groups of sunspots)
`/data/all_256` - (Not included here) 3.4GB of vector magnetogram data from 2010-2013

