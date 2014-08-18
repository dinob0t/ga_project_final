# Investigating the relationship between solar magnetic activity and coronal mass ejections

## Summary

An coronal mass ejection (CME) is an energetic event in which the sun ejects a large body of plasma along with a frozen in magnetic field configuration into the solar wind. A so called 'halo' event occurs when this ejection appears primarily along the Earth-Sun field of view. It is these events in particular which pose risk to Earth because of the strong association with space weather and geomagnetic storms arising from the CME's magnetic interaction with the Earth's magnetic field. This poses problems for astronauts, satellites, high frequency communications, and may induce currents in any long conductors near the Earth's poles (pipelines, powerlines etc.) It is clearly of interest to understand and predict these events.

Because of the strong association of CMEs and the solar magnetic field configuration, a natural place to start looking at predictors is the sun spot cycle (sun spots occur because the twisted magnetic configurations inhibit heat convection and hence the plasma cools appearing dark, especially in hydrogen-alpha line images of the sun). Excellent data on sun spot numbers exists as far back as the 1800s, and more recently the latitude and longitude of sun spot areas on the sun is documented daily. Other indicators of solar activity include the solar irradiance or radio flux (akin to the power output of the sun) which can be observed at the Lyman Alpha line or 10.7cm Hydrogen line, respectively.  Even better are the vector magnetograms that directly image the magnetic field configuration on the sun's surface for which we have images produced every 15 minutes since 2010. Furthermore to train our classifiers we have the LASCO catalogue of CMEs which has documented every (observerable/detectable) CME since 1997.

## Project files
### Analysis
`cmes.ipynb` - looks at the association of more qualitative sun activity measures on predicting CMEs.

`magnetograms.ipynb` - uses vector magnetogram data from 2010-2013 to analyse solar activity and attempt to predict CMEs.

### Data
`issn.md` - international sunspot number record.

`daily_area.txt` - daily area of the sun covered in sunspots.

`lyman_alpha.txt` - daily solar irradiance.

`f10.7.txt` - daily radio flux.

`g*.txt` - Greenwich sunspot grouping data (tracks groups of sunspots).

`/data/all_256` - (Not included here) 3.4GB of vector magnetogram data from 2010-2013.

### Target
`cme_catalogue.md` - List of times and other attributes for all CMEs since 1997. Objective is to predict the number of CMEs in a given time interval.

![alt text](https://github.com/dinob0t/ga_project_final/blob/master/monthly_mean_cmes.png)

## Part 1 - Proxies for solar activity - analysis and prediction

### Known features that correlate with solar activity
1. The number of sun spots
2. The area of the solar disc covered by sun spots
3. The solar irradiance 
4. The solar radio flux



## Part 2 - Vector magnetogram analysis



Original dimensionality / all data / no time_since
0.641176799121
0.425937394356

Reduce dimensionality to 100 / all data / no time_since
0.500161009592
0.499918964912
Reduce dimensionality to 100 / all data / time_since
0.568281704901
0.565537872349
Reduce dimensionality to 100 / both data / no time_since
0.500259467213
0.5
Reduce dimensionality to 100 / both data / time_since
0.61490019672
0.615946052001

SSIM / all data / no time_since
0.5
0.5
SSIM / all data / time_since
0.529790037914
0.532229086478

SSIM / both data / no time_since
0.65747489485
0.671255472966
SSIM / both data / time_since
0.592279662576
0.595695772371


RF - SSIM / both / time_since
0.726747974389
0.725100209575
RF - SSIM / both / no_time_since
0.710660681846
0.706026340431



